# handsoap

A (really) simple SOAP library. It does not depend on a WSDL. All namespaces, operations, actions and headers are 100% within your control.

## Basic Usage

```javascript
const handsoap = require('handsoap');

const url = 'MY URL';
const body = {
  some: {
    data: 'here'
  }
};

const options = {
  httpHeaders: {
    http: 'Header'
  },
  soapHeaders: {
    soap: 'Header'
  },
  namespaces: [
    'MyNameSpace': 'My.Name.Space',
    'MyNameSpace2': 'My.Name.Space.2'
  ]
}

handsoap.request(url, operation, action, body, options, auth).then((response) => {
  // Success
}, (err) => {
  // Error
});

```

## Wrapper Example


```javascript
// definition ES5
const handsoap = require('handsoap');

HandSoapWrapper = function(url, options, auth) {
  this.url = url;
  this.options = options;
  this.auth = auth;
};

HandSoapWrapper.prototype._wrapRequest = function(operation, action, body) {
  return handsoap.request(this.url, operation, action, body, this.options, this.auth);
}

HandSoapWrapper.prototype.myOperation = function(body) {
  const operation = 'ns1:MyOper';
  const action = 'MyAction';
  return this._wrapRequest(operation, action, body);
}


// definition ES6
class HandSoapWrapper {
  constructor(url, options, auth) {
    this.url = url;
    this.options = options;
    this.auth = auth;
  }

  _wrapRequest(operation, action, body) {
    return handsoap.request(this.url, operation, action, body, this.options, this.auth);
  }

  myOperation(body) {
    const operation = 'ns1:MyOper';
    const action = 'MyAction';
    return this._wrapRequest(operation, action, body);
  }
}


// usage
const url = 'MY URL';

const options = {
  httpHeaders: {
    http: 'Header'
  },
  soapHeaders: {
    soap: 'Header'
  },
  namespaces: [
    'MyNameSpace': 'My.Name.Space',
    'MyNameSpace2': 'My.Name.Space.2'
  ]
};

const auth = {
  user: 'user',
  pass: 'pass'
};

const handSoapWrapper = new HandSoapWrapper(url, options, auth);

handSoapWrapper.myOperation(body).then((response) => {
  // Success
}, (err) => {
  // Error
});
```

## @todo

* remove dependency on request
