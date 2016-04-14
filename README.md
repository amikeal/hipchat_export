hipchat_export.py
=================

A simple script to export 1-to-1 messages from HipChat using the v2 API
found at http://api.hipchat.com/v2.

Usage 
------

```python hipchat_export.py [options]```

Options
------
```
  -v                  Run verbosely
  -h, --help          Show this help file
  -u, --user_token    Your API user token
                        *** Generate this token online at
                        https://coa.hipchat.com/account/api ***
```

Example
------
```hipchat_export.py --user_token jKHxU8x6Jj25rTYaMuf6yTe7YpQ6TV413EUkBd0Z -v```

After execution, a `hipchat_export` folder will be created in the current
working directory, and folders will be created for each person it will ask
for 1-to-1 chat history (this list is determined by a dictionary in the `main()`
function). Uploaded binary files will be found in an `uploads` folder, with a
path that partially matches the filepath recorded in the API data (the domain
and common URI path information is stripped).

The message data is stored as the raw JSON file, in files named `0.txt` through
`n.txt`; as many as needed to fetch all the messages between you and that user.

NOTE: HipChat rate limits the API calls you can make with a user token to 100
call every 5 minutes. This script will track how many calls have been made to
the API, and before it hits 100 will insert a 5 minute pause.


Known Issues
--------

As the description says, this is a **simple** script. There are several caveats that
should be considered before you use it:

1. I have only tested this on OSX (El Capitan) using the built-in python 2.7. I can't think of any reason why it wouldn't run elsewhere, but I don't know, as _I haven't tested it_. 
2. Currently, the list of users that the script cycles through looking for 1-to-1 messages to export is hard-coded into a dictionary in the `main()` function. This really should be changed.
3. If the script halts for any reason, there is no mechanism to resume where it left off. You will need to start over again.
4. The only logging is to `stdout` -- if you want to save the activity for you records, I suggest you capture your screen (`tee` is useful if you are on bash).
