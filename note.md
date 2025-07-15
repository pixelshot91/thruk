```
~/c/g/p/thruk (openapi|✔) [1] $ docker run --mount=type=bind,source=.,target=/home/ubuntu/thruk -it ubuntu:24.04 
root@abbbf03f7ff0:/# cd /home/ubuntu/thruk/
root@abbbf03f7ff0:/home/ubuntu/thruk# ./.ci/prepare_machine.sh 
$ su ubuntu
$ bash -x ./.ci/install_deps.sh

ubuntu@0c4852f278ba:~/thruk$ perl -I/home/ubuntu/thruk/lib script/thruk_update_docs_rest.pl 
[ERROR]  at /home/ubuntu/thruk/lib/Thruk/Backend/Manager.pm line 1715.
[ERROR]         Thruk::Backend::Manager::_do_on_peers(Thruk::Backend::Manager=HASH(0x559edbd59548), "get_services", ARRAY(0x559edb314fd8)) called at /home/ubuntu/thruk/lib/Thruk/Backend/Manager.pm line 635
[ERROR]         Thruk::Backend::Manager::get_services(Thruk::Backend::Manager=HASH(0x559edbd59548), "filter", ARRAY(0x559edbd5c638), "columns", ARRAY(0x559edbf78590), "options", HASH(0x559edc6fb110)) called at /home/ubuntu/thruk/lib/Thruk/Controller/rest_v1.pm line 2308
[ERROR]         Thruk::Controller::rest_v1::_rest_get_livestatus_services(Thruk::Context=HASH(0x559edbd5b670), "/services") called at /home/ubuntu/thruk/lib/Thruk/Controller/rest_v1.pm line 475
[ERROR]         Thruk::Controller::rest_v1::_fetch(Thruk::Context=HASH(0x559edbd5b670), "/services", undef) called at /home/ubuntu/thruk/lib/Thruk/Controller/rest_v1.pm line 229
[ERROR]         eval {...} called at /home/ubuntu/thruk/lib/Thruk/Controller/rest_v1.pm line 228
[ERROR]         Thruk::Controller::rest_v1::process_rest_request(Thruk::Context=HASH(0x559edbd5b670), "/services") called at /home/ubuntu/thruk/lib/Thruk/Controller/rest_v1.pm line 180
[ERROR]         Thruk::Controller::rest_v1::index(Thruk::Context=HASH(0x559edbd5b670), "/thruk/r/services") called at /home/ubuntu/thruk/lib/Thruk/Context.pm line 761
[ERROR]         Thruk::Context::sub_request(Thruk::Context=HASH(0x559edbc87690), "/r/services", "GET", HASH(0x559eda4b4208)) called at script/thruk_update_docs_rest.pl line 29
Not an ARRAY reference at script/thruk_update_docs_rest.pl line 29.


# Without my BEGIN {} in Thruk.pm
ubuntu@abbbf03f7ff0:~/thruk$ perl -I/home/ubuntu/thruk/lib script/thruk_update_docs_rest.pl 
[ERROR] Died at /home/ubuntu/thruk/lib/Thruk/Backend/Manager.pm line 1720.
Not an ARRAY reference at script/thruk_update_docs_rest.pl line 29.

# THRUK_VERBOSE=4 perl -I/home/ubuntu/thruk/lib script/thruk_update_docs_rest.pl
```

### 

Need to run naemon, no need to run thruk

Comment disable backend based on group


```
<as naemon> $ THRUK_BACKENDS='ALL' THRUK_VERBOSE=4 perl -I/mnt/thruk/lib/ script/thruk_update_docs_rest.pl

[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ] {
[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ]    "file" : "/mnt/thruk/var/api_keys/45bd1a340f17113397988d5f9077beedb2e5a7e7db6c6882edbd63a038df51e4.SHA-256",
[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ]    "hashed_key" : "45bd1a340f17113397988d5f9077beedb2e5a7e7db6c6882edbd63a038df51e4",
[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ]    "message" : "successfully created api key",
[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ]    "private_key" : "e2eb81f9a746e3d11b3f402c895f1d9334ed6cb17609a89080540c3d76be0e68_1"
[00:27:59,301][I][lib/Thruk/Utils/CLI.pm:372    ] }
malformed JSON string, neither tag, array, object, number, string or atom, at character offset 0 at script/thruk_update_docs_rest.pl line 327.
```

and 'docs/documentation/rest.asciidoc' is still not updated :-(