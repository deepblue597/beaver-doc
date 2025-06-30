# Connection

```
import types

Connector :

    'connector' '{'

       (
        'bootstrap_servers' '=' bootstrap_servers=STRING
        'security_protocol' '=' security_protocol=STRING
        ('sasl_username' '=' sasl_username=STRING)?
        ('sasl_password' '=' sasl_password=STRING)?
        ('quix_sdk_token' '=' quix_sdk_token=STRING)?
        ('consumer_group' '=' consumer_group=STRING)?
        ('auto_offset_reset' '=' auto_offset_reset=STRING)?
        ('commit_interval' '=' commit_interval=FLOAT)?
        ('commit_every' '=' commit_every=INT)?
        ('consumer_poll_timeout' '=' consumer_poll_timeout=FLOAT)?
        ('producer_poll_timeout' '=' producer_poll_timeout=FLOAT)?
        ('loglevel' '=' loglevel=STRING)?
        ('auto_create_topics' '=' auto_create_topics=BOOL)?
        ('use_changelog_topics' '=' use_changelog_topics=BOOL)?
        ('quix_config_builder' '=' quix_config_builder=STRING)?
        ('topic_manager' '=' topic_manager=STRING)?
        ('request_timeout' '=' request_timeout=FLOAT)?
        ('topic_create_timeout' '=' topic_create_timeout=FLOAT)?
        ('processing_guarantee' '=' processing_guarantee=STRING)?
       )#


    '}'

;

```

The Connection entity lets you configure the connection with kafka. The user needs to define 2 variables:

- `bootstrap_servers` -> ip and port of the kafka broker to connect to
- `security_protocol` -> plaintext or sasl. If sasl you also need to define `sasl_username` and `sasl_password`

If an incorrect variable is added Beaver will throw an error.
