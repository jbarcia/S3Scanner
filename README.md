# S3Scanner
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/) [![Build Status](https://travis-ci.org/sa7mon/S3Scanner.svg?branch=master)](https://travis-ci.org/sa7mon/S3Scanner)

A tool to find open S3 buckets and dump their contents :droplet:

![1 - s3finder.py](https://user-images.githubusercontent.com/3712226/36616997-726614a6-18ab-11e8-9dd3-c43715ef7355.png)

## Using

<pre>
#  s3scanner - Find S3 buckets and dump!
#
#  Author: Dan Salmon - @bltjetpack, github.com/sa7mon

positional arguments:
  buckets                Name of text file containing buckets to check

optional arguments:
  -h, --help              show this help message and exit
  -o, --out-file OUTFILE  Name of file to save the successfully checked buckets in (Default: buckets.txt)
  -c, --include-closed    Include found but closed buckets in the out-file
  -r , --default-region   AWS region to default to (Default: us-west-1)
  -d, --dump              Dump all found open buckets locally
  -l, --list              List all found open buckets locally
</pre>

The tool takes in a list of bucket names to check. Found S3 domains are output to file with their corresponding region in the format 'domain:region'. The tool will also dump the contents of 'open' buckets locally.

## Examples
This tool accepts the following type of bucket formats to check:

- bucket name - `google-dev`
- domain name - `uber.com`, `sub.domain.com`
- full s3 url - `yahoo-staging.s3-us-west-2.amazonaws.com` (To easily combine with other tools like [bucket-stream](https://github.com/eth0izzle/bucket-stream))
- bucket:region - `flaws.cloud:us-west-2`

```bash
> cat names.txt
flaws.cloud
google-dev
testing.microsoft.com
yelp-production.s3-us-west-1.amazonaws.com
github-dev:us-east-1
```
	
1. Dump all open buckets, log both open and closed buckets to found.txt
	
	```bash
	> python ./s3scanner.py --include-closed --out-file found.txt --dump names.txt
	```
2. Just log open buckets to the default output file (buckets.txt)

	```bash
	> python ./s3scanner.py names.txt
	```
3. Save file listings of all open buckets to file
    ```bash
    > python ./s3scanner.py --list names.txt

    ```

## Installation
  1. (Optional) `virtualenv venv && source ./venv/bin/activate`
  2. `pip install -r requirements.txt`
  3. `python ./s3scanner.py`

(Compatibility has been tested with Python 2.7 and 3.6)

## Contributing
Issues are welcome and Pull Requests are appreciated. All contributions should be compatible with both Python 2.7 and 3.6.

|    master    |    [![Build Status](https://travis-ci.org/sa7mon/S3Scanner.svg?branch=master)](https://travis-ci.org/sa7mon/S3Scanner)    |
|:------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| enhancements | [![Build Status](https://travis-ci.org/sa7mon/S3Scanner.svg?branch=enhancements)](https://travis-ci.org/sa7mon/S3Scanner) |
|     bugs     |     [![Build Status](https://travis-ci.org/sa7mon/S3Scanner.svg?branch=bugs)](https://travis-ci.org/sa7mon/S3Scanner)     |

### Testing
* All test are currently in `test_scanner.py`
* Run tests with in 2.7 and 3.6 virtual environments.
* This project uses **pytest-xdist** to run tests. Use `pytest -n NUM` where num is number of parallel processes.
* Run individual tests like this: `pytest -q -s test_scanner.py::test_namehere`

## License
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International [(CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
