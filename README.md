# XIQ REST BssidLister (Go)

BssidLister retrieves the list of Access Points and associated (B)SSIDs from [ExtremeCloud IQ](https://extremecloudiq.com/) (XIQ) via the provided REST API and prints CSV to stdout.

## Branches

This project uses two defined branches:

* `master` is the primary development branch. Code within `master` may be broken at any time.
* `stable` is reserved for code that compiles without errors and is tested. Track `stable` if you just want to use the software.

Other branches, for example for developing specific features, may be created and deleted at any time.

## Dependencies

BssidLister uses the modules [godotenv](https://github.com/joho/godotenv), [envordef](https://gitlab.com/rbrt-weiler/go-module-envordef) and [xiqrestclient](https://gitlab.com/rbrt-weiler/go-module-xiqrestclient). Execute...

1. `go get -u github.com/joho/godotenv`
1. `go get -u gitlab.com/rbrt-weiler/go-module-envordef`
1. `go get -u gitlab.com/rbrt-weiler/go-module-xiqrestclient`

...before running or compiling GenericNbiClient. All other dependencies are included in a standard Go installation.

## Running / Compiling

Use `go run ./...` to run the tool directly or `go build -o BssidLister ./...` to compile a binary. Prebuilt binaries may be available as artifacts from the GitLab CI/CD [pipeline for tagged releases](https://gitlab.com/rbrt-weiler/xiq-rest-bssidlister-go/pipelines?scope=tags).

Tested with [go1.13](https://golang.org/doc/go1.13).

## Usage

`BssidLister -h`:

<pre>
Available options:
  -accesstoken string
    	Access token to authenticate with XIQ
  -clientid string
    	Client ID for authentication
  -clientsecret string
    	Client Secret for authentication
  -host string
    	XIQ Hostname / IP
  -ownerid string
    	Owner ID of the XIQ instance to use
  -redirecturi string
    	Redirect URI configured for used app
  -timeout uint
    	Timeout for HTTP(S) connections (default 5)
  -version
    	Print version information and exit

All options that take a value can be set via environment variables:
  XIQHOST           -->  -host
  XIQTIMEOUT        -->  -timeout
  XIQOWNERID        -->  -ownerid
  XIQACCESSTOKEN    -->  -accesstoken
  XIQCLIENTID       -->  -clientid
  XIQCLIENTSECRET   -->  -clientsecret
  XIQREDIRECTURI    -->  -redirecturi

Environment variables can also be configured via a file called .xiqenv,
located in the current directory or in the home directory of the current
user.
</pre>

## XIQ Hostname

In order for BssidLister to work, it is not possible to use extremecloudiq.com as the host to connect to. Instead, you must use the regional hostname of the XIQ instance you want to access.

After logging in to the XIQ instance you want to access with BssidLister, have a look at the hostname displayed in the address bar (for example fra.extremecloudiq.com or va2.extremecloudiq.com). This is the one you need for BssidLister.

## Authentication

BssidLister uses the OAuth authentication model provided by XIQ's API. Authentication requires Client ID, Client Secret, Redirect URI, Owner ID and Access Token. You will need to access the [Developer Portal](https://developer.aerohive.com/) and [ExtremeCloud IQ](https://extremecloudiq.com/) in order to obtain all required pieces of information.

1. Client ID, Client Secret and Redirect URL:
   * After logging in to the Developer Portal, click on _Create new application_. After creating the application, both Client ID and Client Secret will be provided.
   * Next, enter a _Redirect URL_ for your application - which will be used as Redirect URI during authentication - and click on submit. Please note the the Redirect URL is only used for authentication by BssidLister, not for actual redirects.
1. Owner ID: After logging in to the XIQ instance you want to access with BssidLister, hover over your name in the upper right corner and click on _About ExtremeCloud IQ_. The _VIQ ID_ listed in the about window is the Owner ID.
1. Access Token: After logging in to the XIQ instance you want to access with BssidLister, hover over your name in the upper right corner and click on _Global Settings_. Within the Global Settings, navigate to _API Token Management_. Create a new API Access Token with the plus sign and you will receive the required Access Token. Please note that the Client ID for the API Access Token must match the Client ID obtained in step 1.

## Source

The original project is [hosted at GitLab](https://gitlab.com/rbrt-weiler/xiq-rest-bssidlister-go), with a [copy over at GitHub](https://github.com/rbrt-weiler/xiq-rest-bssidlister-go) for the folks over there.
