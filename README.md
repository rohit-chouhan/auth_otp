# Auth TOTP

A fast and easy-to-use time-based one-time password (TOTP) authentication package for your Flutter application. It is compatible with `Google Authenticator`, `1Password`, `LastPass`, `Microsoft Authenticator` and various other authenticator apps.

![Auth TOTP Banner](https://github.com/rohit-chouhan/auth_otp/assets/34239087/f22d91d0-452c-473a-87b7-a26107985df1)

## Get Started

- [🔑 Create Secret Key](#create-secret-key)
- [✔️ Verify TOTP Code](#verify-totp-code)
- [🚀 Generate TOTP Code](#generate-totp-code)
- [📸 Get QR Code to Scan](#get-qr-code-to-scan)
- [🔐Tested Authenticator Apps](#tested-authenticator-apps)
- [🔐 Full Example](#full-example)
- [🐛 Report bugs or issues](#report-bugs-or-issues)

## Create Secret Key

🔑 This method generates a random `Base32` secret key, which is used to create verify codes from authentication apps.

```dart
String secret = AuthOTP.createSecret(); //32 charater by default
//or
String secret = AuthOTP.createSecret(20); //with length limit 20 charater
```

This method accepts a single parameter to specify the length of the secret key. By default, it generates a 32-character Base32 secret key. The length limit is between `16` to `32` characters.

## Verify TOTP Code

✔️ This method verifies a Time-based One-Time Password (TOTP) code using the secret key and the TOTP code generated by your `authenticator app`.

Use this method after the user has scanned a QR code or entered the secret key into the authentication app. The same secret key generated by `createSecret` and the TOTP code generated by the `authenticator app` should be passed here to verify.

```dart
bool checkOTP = verifyCode({
    secretKey: "secret_key_here",
    totpCode: "totp_code_here_by_user"
});
```

- `secretKey`: A secret key generate by createSecret method
- `totpCode`: The TOTP code entered by the user.

It will return true if code is correct, otherwise false.

## Generate TOTP Code

🚀 This method generates a TOTP code based on the secret key and the time interval. The time interval is specified in seconds.

```dart
String generatedTOTPCode = AuthOTP.generateTOTPCode(
    secretKey: 'secret_key_here',
    interval: 30
);
```

- `secretKey`: A secret key generate by createSecret method
- `interval`: Time interval in seconds, ex. 30

As well as you can use this method to verify TOTP code also.

#### Example Code:-

```dart
String generatedTOTPCode = AuthOTP.generateTOTPCode(
    secretKey: 'secret_key_here',
    interval: 30
);

String inputedOTP = "otp_inputed_by_user";

if(generatedTOTPCode === inputedOTP){
    print("Verified")
} else {
    print("Not Verified")
}
```

## Get QR Code to Scan

📸 This method returns a QR code URL to scan with your authenticator app. It can be used in `Image.Network()`

```dart
String qrCodeUrl = getQRCodeUrl({
    appName: "your app name"
    secretKey: "secret_key_here",
    issuer:"auth_otp"
});

//Image.Network(qrCodeUrl);
```

- `appName`: App name, or any text
- `secretKey`: A secret key generate by `createSecret` method
- `issuer`: Issuer name, default is `auth_otp`

## Tested Authenticator Services

🔐
|Logo | Service Name | Status |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | ------ |
| <img width="40" src="https://play-lh.googleusercontent.com/NntMALIH4odanPPYSqUOXsX8zy_giiK2olJiqkcxwFIOOspVrhMi9Miv6LYdRnKIg-3R=w480-h960-rw"/> | Google Authenticator | ✅ |
| <img width="40" src="https://play-lh.googleusercontent.com/RyPWI5dSfKqMUnuEYqMqQPMLv8AvKehIhut1yIKJU91HWpvtUHPj1rzn_UHwpEqH2a0=w480-h960-rw"/> | 1Password | ✅ |
| <img width="40" src="https://play-lh.googleusercontent.com/BPgJq2T40gw219T9wcXPld0urrii1L9WwGZ0xovChB7fy-KFfVlKPE6oT5D7lIeQRecJ=s96-rw"/> | LastPass | ✅ |
| <img width="40" src="https://play-lh.googleusercontent.com/_1CV99jklLbXuun-6E7eCPR-sKKeZc602rhw_QHZz-qm7xrPdgWsJVc7NtFkkliI8No=w480-h960-rw"/> | Microsoft Authenticator | ✅ |

Absolutely, it works with all authenticator apps. But feel free to contribute if you have tested it with any other authenticator app.

## Full Example

👉 For a complete example, refer to the [Auth OTP package documentation](https://pub.dev/packages/auth_otp/example).

## Report bugs or issues

🐛 You are welcome to open a _[ticket](https://github.com/rohit-chouhan/auth_otp/issues)_ on github if any 🐞 problems arise. New ideas are always welcome.

> Copyright © 2024 **[Rohit Chouhan](https://rohitchouhan.com)**. Licensed under the _[MIT LICENSE](https://github.com/rohit-chouhan/auth_otp/blob/main/LICENSE)_
