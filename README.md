# Nativescript Hosted Device
This a Nativescript Plugin that lets you access device information from a hosted Angular 2 application.

## Installation

```
tns plugin add nativescript-hosted-toast

```

 ## Usage

Create a wrapper application with the following code and a Navivescript WebView.
See the following project as an example:
https://github.com/Ulbora/NSWrapper

```
var application = require("application");
function pageLoaded(args) {
    var page = args.object;   
    var web = page.getViewById("webView"); 
    var androidSettings = web.android.getSettings();
    androidSettings.setJavaScriptEnabled(true);
    var device = new com.ulbora.device.Device;    
    web.android.addJavascriptInterface(device, 'NSDevice');    
    web.url = "http://someURLWhereAngular2AppIsHosted";
}
exports.pageLoaded = pageLoaded;

```

Inside the Angular 2 hosted application, write the code where you want to access device information.
See the following project as an example:
https://github.com/KenWilliamson/Angular2HostedMobileApp

component code:
```
 ngOnInit() {
        this.id = this._routeParams.get('id');
        this.hero = this._heroDetailsService.getHeroDetails(this.id);     
        try {
            if (NSDevice) {
                this.deviceReady = true;
            }
        } catch (err) {
        }
    }


onShowDevice() {
        try {            
            this.dev = "Mobile version: " + NSDevice.getModel();
        } catch (err) {
            alert('Failed because: ' + err);
            this.error = err.message;
        }
    }

```

Template Code:
```
<div *ngIf="deviceReady">
    <div> <b>Your device</b>: <span (click)="onShowDevice()" class="glyphicon glyphicon-phone"></span></div>
</div>

```

## Available Methods
#### NSDevice.getModel()
Returns build information about the device
#### NSDevice.getProductName()
Returns product name of the device
#### NSDevice.getManufacturer()
Returns manufacturer information for the device
#### NSDevice.getSerialNumber()
Returns serial number of the device
#### NSDevice.getOSVersion()
Returns OS version of the device
#### NSDevice.getPlatform()
Returns the device platform

