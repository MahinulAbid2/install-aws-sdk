# Reason for creating this reademe
* The AWS documentation contains many many information.
* This makes it hard for me to actually understand what is the right way to integrate `aws-sdk` in the project.
* I already know a way but that way is obsolete.
* It still do the job but keeps giving me a warning message that `it is deprecated`.
* Plus, there are no proper documentation of `aws-sdk` in website fetched by google.
* Everyone keeps discussing about `lambda`
* That's why I decided to research about it and fetch notes from those vast documentation.

<br>
<br>

#### Install `aws-sdk v2` which is outdated
```console
npm install aws-sdk
```

<br>

```javascript
// import and work with aws v2

const AWS = require( 'aws-sdk' );

AWS.config.update({
  accessKeyId: 'AKIAUYPP6YV4XQS665GF',
  secretAccessKey: '9TND7wbQ8GCMeAFSOvPNrz0+k1gGdrZHJ2IHMizT',
  region: 'ap-south-1' // Change to your AWS region
});

// initialize s3
const s3 = new AWS.S3();


 s3.putObject({
    Body: imageFile,  //file read with fs.readFile
    Key : `${uploadDestination}/${uniqueKey}.jpg`,  // do not start with "/", it will create a file with name "/"
    Bucket: 'knigiimagedb',
    ACL: "public-read",  // so that it can be publicly accessible

}, ( err ) => {
    if( err ) {
        console.log( err ) 
    } else{
        console.log(`File upload Successful. Time took: ${ this.executionTime }ms`);
    } 
});
```


<br>
<br>
<br>

### install aws-sdk v3
* I'm guessing this will stop giving me the outdated warning.
* It has a different way of installing.
* To install a service from the AWS SDK for JavaScript using npm, the Node.js package manager, enter the following command at the command prompt, where `SERVICE` is the name of a service, such as `s3`

```console
npm install @aws-sdk/client-SERVICE
// replace the "SERVICE" with aws desired service. for example s3


npm install @aws-sdk/client-s3
```

<br>
<br>

#### now how do I implement the S3? in node.js/express.js
```console
npm install @aws-sdk/client-s3
```

```javascript
const { S3 } = require('@aws-sdk/client-s3');

// initialize s3
const s3 = new S3({
    credentials: {
        accessKeyId: 'AKIAUYPP6YV4XQS665GF',
        secretAccessKey: '9TND7wbQ8GCMeAFSOvPNrz0+k1gGdrZHJ2IHMizT'
    },

    // Change to your AWS region
    region: 'ap-south-1'
});
/*
- what changed is
- I only require S3 instead of full AWS from aws-sdk
- In version 2 = I need AWS.config.update() to put initial credential
- I can put credential using just S3 like above in version 3.
- It improves the performence for just importing only what I need.
*/


// rest is just like before.
s3.putObject({
    Body: imageFile,  // file read by fs.readFile
    Key : `${uploadDestination}/${uniqueKey}.jpg`,  // do not start with "/", it will create a file with name "/"
    Bucket: 'knigiimagedb',
    ACL: "public-read",

}, ( err ) => {
    if( err ) {
        console.log( err ) 
    } else{
        console.log(`File upload Successful. Time took: ${ this.executionTime }ms`);
    } 
});

```
