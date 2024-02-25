# gamin-backup

Script to backup your activities from Garmin to the local disk. It uses the API from [GaminConnect](https://github.com/cyberjunky/python-garminconnect) to authenticate, store the session credentials, and download data from Garmin site.

**Why create this script?**

I am implementing a functionality similar to other available tools, such as [garminexport](https://github.com/petergardfjall/garminexport) or [garpy](https://github.com/felipeam86/garpy), both of which I have been using until Garmin Connect changed the authentication method and these scripts have stopped working. This is why I have implemented ``garmin-backup``, using the GarminConnect API that works now. Besides that, I've added a functionality that I missed from the other two scripts: the limitation on dates. This allows me to store my data in different folders per year, rather than having all activities in a single folder, which as becoming a bit too many over the years.

Note this is just using a very limited subset of GarminConnect, only focused at downloading the activity data for now. Maybe later other data will be added, but I'm not really interested in extracting other data.

This is the first working version, but not really final. I still need to implement the functionality to download activities by id. The rest is pretty much working, and the user gets some descriptive This version also allows to use a FakeGarmin class for test purposes, so it does all the steps without really making any connection to GarminConnect, just using some activity data I've downloaded.


## Installation

Just clone or download the repository, create a virtual environment with the requirements, and that's it. You need to have python installed in your environment.

```bash
git clone https://github.com/osso73/garmin-backup.git
cd garmin-backup
python -m venv .venv
.venv/Scripts/activate.bat   # for linux use: source .venv/bin/activate
pip install -r requirements.txt
```

That's it, you can run the program in `src/garmin-backup`:

```bash
cd src
python garmin-backup data  # see the usage below for all the available options
```



## Usage

    gamin-backup is a script to download your activities from 
    Garmin Connect, so you can keep a local copy in your computer.

    Usage: garmin-backup [options] <path>

    <path>                    Activity folder to store your activities.


    Options:
    -f, --formats=FORMAT      Which formats to download [default: gpx].
                              Choose from the available options: 
                              original|gpx|csv|tcx|kml. You can have more than 
                              one format by separating them by spaces, and in "".
    -u, --username=USERNAME   Username of your Garmin account
    -p, --password=PASSWORD   Password of your Garmin account
    -a, --activity=ID         Activity ID. Download only that activity, even 
                              if it has already been downloaded. Yoy can add
                              several IDs separated by space, and in "".
    -s, --start=S_DATE        Start date, in ISO format. If only the year is
                              provided, it will assume Jan 1st of that year.
    -e, --end=e_DATE          End date, in ISO format. If only the year is
                              provided, it will assume Dec 31st of that year.
    --fake                    Use fake data, instead of connecting to Garmin.
                              For test purposes only.
    --help                    Show this message and exit.
    --verion                  Show the version and exit.

    The username and password can also be provided through environment variables 
    USER and PASSWORD. If not provided through command line or environment 
    variables, the program will prompt for this information the first time. The 
    credential information will then be stored in .garminconnect folder under user
    profile, and re-used for the future, until they need to be refreshed.

    All activities between S_DATE and E_DATE that are not already present in <path> 
    will be downloaded. If no dates are provided, it will assume all activities, 
    from the beginning until today.

    There is a limit of 100 activities at a time, in order to avoid overloading
    the Garmin Connect page, and getting banned. If you have more than 100 
    activities to download, you can just run the program again.



## License

This project is using an MIT license.