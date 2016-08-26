Classy
======

Classy is a simple [Flask][] app which demonstrates one
possible use of the Classes API.

Here's a screenshot:

<img src="images/screenshot.png" alt="ANS207 is meeting right now in Withycombe Hall.&#10;&#10;Instructor: Johnson, Janell&#10;&#10;Meeting times:&#10;    * M 1400-1500 WITH 217&#10;    * M 1600-1720 WITH 217&#10;&#10;That's about it for Animal Sciences courses right now. Try again later or try a different subject.">

[Flask]: http://flask.pocoo.org/

Installation
----

    git clone https://github.com/osu-mist/classy-demo.git
    virtualenv classy-demo
    cd classy-demo
    bin/pip install -e .

Configuration
----

Register an application to use the
Class Search API, Course Subjects API, and Terms API
at the [OSU Developer Portal][].

Create a file called config.py containing your Client ID 
and Client Secret.

    CLIENT_ID="yourclientid"
    CLIENT_SECRET="yourclientsecret"

[OSU Developer Portal]: https://developer.oregonstate.edu/

Testing
----

    % bin/python -m classy.tests

This will run the unit tests for Classy.

Running
----

    % CLASSY_CONFIG=../config.py bin/python -m classy

Note that the path to the configuration file in `CLASSY_CONFIG`
is relative to the package directory (./classy in this example).

Docker
----

### Building a docker image

    # docker build --tag=classy .

This builds a docker image containing classy and all its dependencies.

### Running the docker container

    # docker run -p 5001:8000 -e CLASSY_CLIENT_ID=xxx -e CLASSY_CLIENT_SECRET=xxx classy

This runs the container and passes it the api credentials via environment variables.
The `-p` option forwards port 5001 on the host machine to port 8000 inside the container.
The `-e` option sets an environment variable.
The last argument is the tag we specified when building the image.

    # docker run -p 5001:8000 -v "$PWD"/config.py:/src/config.py:ro -e CLASSY_CONFIG=/src/config.py classy

You can also supply a config file from outside the container.
The `-v` option mounts ./config.py into the container as /src/config.py.

BUGS
----

 * retrieves the full course list on every request; should add some caching
 * could be smarter about choosing random subjects and courses
 * doesn't understand that finals only meet during finals week
