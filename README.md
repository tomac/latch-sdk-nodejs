### latch-sdk-nodejs ###


#### Prerequisites ####

* NodeJS.

* Read API documentation (https://latch.elevenpaths.com/www/developers/doc_api).

* To get the "Application ID" and "Secret", (fundamental values for integrating Latch in any application), it’s necessary to register a developer account in Latch's website: https://latch.elevenpaths.com. On the upper right side, click on "Developer area".


#### Using the SDK in NodeJS ####

* You need to include the npm package 'latch-sdk' in your package.json file and then require the "latch-sdk" in your NodeJS file.
```
    var latch = require('latch-sdk);
```

* Initialize latch with your AppId and SecretKey
```
    latch.init(appId, secretKey);
```

* Optional settings:
```
	latch.setHost(LATCH_HOST);
```

* Call to Latch Server. Pairing will return an account id that you should store for future api calls
```
     var pairResponse = latch.pair(PAIRING_CODE, function(data) {
             if (data["data"]["accountId"]) {
                 saveAccountIdForUserId(req.user.id, { accountId: data["data"]["accountId"] }, function(err) {
                     if (err) { return next(err); }
                 });
                 res.redirect("/");
             } else if (data["error"]) {
                 var message = "There has been an error with Latch, try again";
                 res.render("setup", { user: req.user, message: message, accountId: "" });
             }
     });
     
     var statusResponse = latch.status(YOUR_ACCOUNT_ID, function(data) {
         console.log(data);
     });
```
