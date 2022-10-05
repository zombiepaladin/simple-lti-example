# Simple LTI Example

This program implements the IMS LTI 1.1 standard [see developer's guide](https://www.imsglobal.org/specs/ltiv1p1/implementation-guide) to act as a Learning Tool with a Learning Management System like Canvas, Blackboard, or Moodle.

## Getting Started

First, clone the project into your development environment.

### Configuration
The LTI 1.1 standard uses OAuth 1.0 to authenticate requests between the Learning Tool (this app) and the Learning Management System. This requires two pieces of data to be shared between the two platforms - a _client key_ and a _shared secret_.  

For this example application, these need to be stored in the environment variables
`CLIENT_KEY` and `SHARED SECRET`, respectively.  And easy way to do this in a development environment is to add a file named _.env_ with those two keys.  An example can be seen in [example.env](example.env) in this project - you can even rename it to _.env_.  However, you should change the key and secret to something new.  Note that git will ignore (and not commit) your _.env_ files.  This is by design - you do not want to share your key or secret in a public repository!

In a larger application working with multiple LMS instances, you would instead use a separate key/secret pair for each, and store them persistently (such as in a database).

### Installing Dependencies

Dependencies can be installed with the command:

```$ npm install```

### Starting the Server

The program can then be launched with the command:

```$ npm start```

The server will then be running locally on port 3000 (or the one specified by the PORT environment variable).

### Proxying with ngork

While you could now make requests against your server at http://localhost:3000, most LMS systems disallow localhost as a valid host for security reasons. If this is the case for you, you will need to proxy your request through a server with a dedicated ip address. The [ngrok](https://ngrok.com/) tool can be used for this.

Once you have signed up for and installed ngrok, you can start the proxy with:

```
$ ngrok http 3000
```

If you have changed the port the app is running on, replace 3000 with the new port number.  The output from ngrok will include a https address you can use for your LMS launch url.

Finally, because you are now proxying your application, you will need to add an environment variable `TRUST_PROXY` to indicate to the app that it is intended to be running behind a proxy server.  The value can either be `true` or the ip address of the proxy server.