# gun

[https://app.popdoc.io/kevin/gun-database/5f179480fe3043315e8a3c1d](https://app.popdoc.io/kevin/gun-database/5f179480fe3043315e8a3c1d)

[https://gun.eco/docs/API#-a-name-open-a-gun-open-callback-](https://gun.eco/docs/API#-a-name-open-a-gun-open-callback-)

[https://gun.eco/docs/RAD](https://gun.eco/docs/RAD)

[https://gun-iris.herokuapp.com/#/settings](https://gun-iris.herokuapp.com/#/settings)

[https://github.com/GiraffeKey/griffin](https://github.com/GiraffeKey/griffin)

[https://github.com/amark/gun/wiki/Awesome-GUN](https://github.com/amark/gun/wiki/Awesome-GUN)

[https://github.com/cabal-club/cabal-core](https://github.com/cabal-club/cabal-core)

[https://stackoverflow.com/questions/49855267/disconnecting-a-gun-peer](https://stackoverflow.com/questions/49855267/disconnecting-a-gun-peer)

[https://medium.com/@ajmeyghani/data-modeling-with-gundb-15220cbfb8da](https://medium.com/@ajmeyghani/data-modeling-with-gundb-15220cbfb8da)

[https://github.com/amark/gun/blob/master/test/panic/load.js](https://github.com/amark/gun/blob/master/test/panic/load.js) PANIC

[https://github.com/diatche/gun-util#GunUser](https://github.com/diatche/gun-util#GunUser)

- changepswd

```jsx
const changePasswordWithPriv = this.changePasswordWithPriv = async (pub, priv, epriv, newPassword) => {
  const id = `~${pub}`
  const key = 'auth'
  const salt = Gun.text.random(64)
  const proof = await new Promise(res => SEA.work(newPassword, salt, res))
  const encrypted = await new Promise(res => SEA.encrypt({ priv, epriv }, proof, res, {raw: 1 }))
  const value = JSON.stringify({ek: encrypted, s: salt})
  const signed = await SEA.sign(
      {
        "#": id,
        ".": key,
        ":": value,
        ">": Gun.state()
      },
      { priv, pub }
    )
  return await gun
    .get(id)
    .get(key)
    .put(signed)
    .then()
};
```

- changepswd 2021

```jsx
const changePasswordWithPriv = this.changePasswordWithPriv = async (pub, priv, epriv, newPassword) => {
  const id = `~${pub}`
  const key = 'auth'
  const salt = Gun.text.random(64)
  const proof = await new Promise(res => SEA.work(newPassword, salt, res))
  const encrypted = await new Promise(res => SEA.encrypt({ priv, epriv }, proof, res, {raw: 1 }))
  const value = JSON.stringify({ek: encrypted, s: salt})
  const signed = gun.user().is ? value : null;
  if(!signed) return alert ("fug, cannot write without signing in with the pair");
  return await gun
    .get(id)
    .get(key)
    .put(signed)
    .then()
};
```

- inbox


```jsx
// Alice SENDING TO Bob's inbox
//   The @ symbol is merely a convention. It does not
//   provide any special functionality (the # symbol does though)
var bobsInbox = `@${bobsPubKey}#`;
var myKeypair = await SEA.pair();
var shared = await SEA.secret(bobsEPubKey, myKeypair);
var data = 'secret hello message';
var encData = await SEA.encrypt(data, shared);
var payload = JSON.stringify({ msg: encData, epub: myKeypair.epub });
var hash = await SEA.work(payload, null, null, { name: 'SHA-256' });
gun.get(bobsInbox).get(hash).put(payload);

// Bob READING FROM his inbox
var myInbox = `@${myKeypair.pub}#`;
gun
  .get(myInbox)
  .map()
  .once(async (node, hash) => {
    var payload = JSON.parse(node);
    var shared = await SEA.secret(payload.epub, myKeypair);
    var decMsg = await SEA.decrypt(payload.msg, shared);
    console.log(decMsg);
  });
```

- URL safe hashes


`(async ()=>{
  message = await SEA.work('hello!',null,null,{name:"SHA-256",encode:'hex'})
  console.log(message);
})()
-> ce06092fb948d9ffac7d1a376e404b26b7575bcc11ee05a4615fef4fec3a308b`

****[17:38] jabis:** url-safe base64 snippets from one of my libs

`function encode(buffer) {
  return buffer.toString('base64')
    .replace(/\+/g, '-') // Convert '+' to '-'
    .replace(/\//g, '_') // Convert '/' to '_'
    .replace(/=+$/, ''); // Remove ending '='

}
function decode(base64) {
  // Add removed at end '='
  base64 += Array(5 - base64.length % 4).join('=');
  base64 = base64
    .replace(/\-/g, '+') // Convert '-' to '+'
    .replace(/\_/g, '/'); // Convert '_' to '/'

  return new Buffer(base64, 'base64');
}`

- skyfall user

```jsx
function create({handle, pass, firstname, lastname, email}) {
  var user = new Promise((res, rej) => {
    db.user().create(handle, pass, async (ack) => {
      if (ack.err) {
        return rej(ack.err);
      } else {
        console.log(ack)
        await net.get("users").set({pub : ack.pub}, console.log)
          window.sessionStorage.setItem("user", ack.pub);
          await auth({alias : handle, pass : pass}).then((ack) => {
            console.log(ack)
            var AuthBio = {
              handle : handle,
              firstname : firstname,
              lastname : lastname,
              coverPhoto : "",  
              avatar : "",
              email: email,
              pub : ack.put.pub,
            }
            db.user()
            .get("Bio", (ack) => {
              console.log(ack)
            })
            .put(AuthBio, (ack) => {
              if (ack.err) {
                console.log(ack);
                return rej(ack);
              } else {
                console.log(ack);
                return res(ack);
              }
            });
          })
        return res(ack);
      }
    });
  });

  return user;
}
```

- immutable link to mutable user node MY

```jsx
let message = 'hello world!!!'
let userPub = gun.user().is.pub
gun.user().get('messages').set(message).on(async (data,key)=> {
  let hash = await SEA.work(key,null,null,{name:'SHA-256'})
  gun.get('#messages').get(userPub+'#'+hash).put(key)
})

gun.get('#messages').get({'.':{'*':userPub}}).map().once(data => {
  gun.user(userPub).get('messages').get(data).once(d=> {
    console.log(d, d==message) // 'hello world!!!', true
  })
})
```

- friend requests by Aethiop

```jsx
const addFriend = () => {
        setLoading(true);
        console.log("LOADING")    
        app.get("profiles").map(user => user.username === query ? user: undefined).once(async ack => {

            const taggedUsername = ack.username;
            const pub = ack.pub;
            var username = ""
            setFriends([...friends,[taggedUsername, pub]])
            gun.user(pub).get("profile").get("username").on(ack => {
                console.log("FOUND BY KEY: ", ack)
                username += ack;
            })
            const address = await sendRequest(pub, taggedUsername);

            gun.get(`@${pub}`).get("requests").get(pub).put(address);
            // sendRequest(ack.pub);
        });
        console.log("USER COULD NOT BE FOUND")

        setLoading(false);
        console.log(friends)
    }

    const sendRequest = (pub, userTagged) => {
        var address = new Promise(async (resolve, reject) =>  {
            var certificate = await SEA.certify([pub], [{"*": "chats/inbox", "+": "*"}], user.keyPair, null, {blacklist: 'blacklist'});
            console.log(certificate);
            const friend = gun.get(pub).put({username: userTagged, pub: pub, mutual: 0, certificate: certificate});
            me.get("friends").set(friend).once(async (data, key) => {
                console.log("DATA: ", data)
                let hash = await SEA.work(key, null, null, {name: 'SHA-256'});
    
                app.get("#friendRequests").put(`${user.keyPair.pub}#${hash}`);
    // ERROR HERE, WRONG PUT !!!
                resolve(`${user.keyPair.pub}#${hash}`)
            });
        })

        return address
    }

    gun.get("@"+user.keyPair.pub).get("requests").map().once(data => {

            if (data) {
                
                const [pub, key] = data.split("#")
                
                console.log("PUB: ", pub)  //BOTH WERE FETCHED CORRECTLY ON THE OTHER PEER WHEN ADDED
                console.log("KEY: ", key)
    
            }
        })
```

- disconnect peers

```jsx
this.gun = Gun({
            peers: ['https://' + gundb_origin + "/gun"] ,
            retry: -1,
});
...
var mesh = this.gun.back('opt.mesh');
        var peers = this.gun.back('opt.peers');
        Object.keys(peers).forEach(id => {
            mesh.bye(id)
        });
        window.setTimeout(() => {
            var mesh = this.gun.back('opt.mesh');
            var peers = this.gun.back('opt.peers');
            Object.keys(peers).forEach(id => {
                mesh.bye(id)
            }); 
            this.gun = undefined
        }, 5000);
```

- USER create - recall

create(alias, pass, cb, {already: true

```jsx
gun.user().recall({ sessionStorage: true }, (ack) => {
  gun.get(ack.soul).once(user => console.log(user.alias))
})
```

- LEX

```jsx
// Insert the message at precise current time
gun.get('myapp').get('2021/02/03 00:37:00').set(theMessage)

// Retrieve all messages after some past time (2 hours ago)
gun.get('myapp').get({ '.': { '>': '2021/02/02 22:37:00' } }).map().on(message => /* do something with message */)
```

- DEC-ENC

```jsx
const decEnc = this.decEnc = async(...args)=> {
  let data = args.length > 0 ? args.shift() : false; // data as first argument
  let pair = args.length > 0 ? args.shift() : false; // pair to use in decrypting/encrypting as second argument
  let mode = args.length > 0 ? args.shift() : "decrypt"; // mode optional encrypt/decrypt on SEA defaults to decrypt
  //TODO return Promise.reject if we don't have all mandatory arguments passed
  let secret = await SEA.secret(pair.epub, pair);
  let it = await SEA[mode](data, secret);
  return it;
};

here a fast wrapper for encrypting/decrypting data with keypairs
usage
(async ()=>{
var pair = await SEA.pair(); // you could use gun.user()._.sea if logged in 
var data = {hello:'world'};
var encrypted = await decEnc(data,pair,"encrypt");
console.log("encrypted",encrypted);
var decrypted = await decEnc(encrypted,pair); // mode defaults to decrypt if not passed 
console.log(decrypted) //{hello:'world'}
})()
```