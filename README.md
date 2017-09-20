# Parse f5 syslog

F5 syslog parser is messed up. Needed to modify the Ansible 2.4 network parser
and create a template to create a fact that makes sense.

Given the following
```
my name is {
  blue green
}
sys syslog {
    remote-servers {
        mysyslog1 {
            host 10.1.1.1
        }
        mysyslog2 {
            host 10.1.1.2
        }
        mysyslog3 {
            host 10.1.1.3
        }
        mysyslog4 {
            host 10.1.1.4
        }
    }
}
my name is {
  blue sdfsdfsdf
}

```


It will output

```
ok: [localhost] => {
    "ansible_facts": {
        "syslog_host": [
            {
                "ip": "10.1.1.1",
                "name": "mysyslog1"
            },
            {
                "ip": "10.1.1.1",
                "name": "mysyslog2"
            },
            {
                "ip": "10.1.1.1",
                "name": "mysyslog3"
            },
            {
                "ip": "10.1.1.1",
                "name": "mysyslog4"
            }
        ]
    },
    "changed": false,
    "failed": false
}

```

## License
MIT

## Author

Stanley Karunditu
