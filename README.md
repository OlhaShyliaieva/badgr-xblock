# Badgr Xblock

The badgr-xblock was developed to work in conjunction with the open source [Badgr Server](https://github.com/concentricsky/badgr-server) application or the hosted version at [Badgr.io](https://badgr.io), developed by [Concentric Sky](https://concentricsky.com).

The badgr-xblock communicates with the Badgr API, and awards badges based on a passing grade for a specified subsection in a course. 


Visit [Badgr's API Documentation](https://api.badgr.io/docs/v2/) for more information.

## Installation
```
$ sudo su edxapp -s /bin/bash
$ cd ~ && source edxapp_env
$ cd /edx/app/edxapp/edx-platform
$ pip install -U -e git+https://github.com/proversity-org/badgr-xblock#egg=badgr-xblock
$ exit && /edx/bin/supervisorctl restart edxapp:
```

## Setup

Add the following to ```SETTINGS``` and ```XBLOCK_SETTINGS``` inside ```lms.env.json```:

```
BADGR_API_TOKEN: "*****************************************"
BADGR_BASE_URL: "https://badgr.io/"
BADGR_ISSUER_SLUG: *Your oganisation's issuer slug goes here*

"XBLOCK_SETTINGS": {
        "BadgrXBlock": {
            "BADGR_API_TOKEN": "*****************************************",
            "BADGR_BASE_URL": "https://badgr.io/"
        }
    },
```

Then add your ```xblock``` on ```Advanced Settings``` of the course as ```badgr``` in ```Advanced Module List```

## Notes

### The badgr-xblock has several editable fields which are used to obtain and issue badges using the Badgr Server API. 

* The unique lower case ‘Issuer’ name [as configured in Badgr Server](https://badgr.io/issuer)
* Badge name, which corresponds to a unique lower case badge *SLUG*
* Pass mark (minimum grade required for the **graded** subsection in a course)
* Section title (the name of the subsection for which the badge is awarded, all subsections in a course must have unique names)


If you intend to use this xblock whilst having multiple issuers for your Open EdX Instance, then you will need to implement the changes [in this commit](https://github.com/proversity-org/edx-platform/commit/422cd1586044cd462356467d11530522792528d) to the badges app in [edx-platform](https://github.com/edx/edx-platform).
