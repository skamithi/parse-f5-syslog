# Parse f5 syslog config

This is an example of using the new Ansible 2.4 network parser to parse out the syslog F5 config into something useful.

First you have to run f5 show config config to print out "single lines". Then run that through grep and look for the word
"syslog".

After that run it through the f5 network parser using the Ansible 2.4 network parser syntax.

Given the following
```
my name is { blue green }
sys syslog { remote-servers { mysyslog1 { host 10.1.1.1 } mysyslog2_yah { host 10.1.1.2 } mysyslog3.yah { host 10.1.1.3 } mysyslog4-yah { host 10.1.1.4 } } }
my name is { blue sdfsdfsdf }

```


It will output

```
"ansible_facts": {
        "syslog_host": {
            "sysloghosts": [
                {
                    "ip": "10.1.1.1",
                    "name": "mysyslog1"
                },
                {
                    "ip": "10.1.1.2",
                    "name": "mysyslog2_yah"
                },
                {
                    "ip": "10.1.1.3",
                    "name": "mysyslog3.yah"
                },
                {
                    "ip": "10.1.1.4",
                    "name": "mysyslog4-yah"
                }
            ]
        }
    },


```

## License
MIT

## Author

Stanley Karunditu
