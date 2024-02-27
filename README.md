# Mongo-Emitter

MongoDB
-------

We use a MongoDB database to store the data collected from running
simulations via the `DatabaseEmitter` class. The use of this class is specified in the
`'emitter'` section of the instance declaration for a given process as such:
    
    ...,
    'emitter': {
                    '_type': 'step',
                    'address': 'local:database-emitter',
                    'config': {
                        'ports': {
                            'inputs': {
                                'table': 'string',

. This can be a remote server, but for this guide we will
run a MongoDB server locally.

**Note**: MongoDB is only required if you want to store data in MongoDB
or want to run experiments that do so via the declaration shown above. You don't need MongoDB to work
through this guide.

*Check Installation*

    $ mongod --version
    db version v4.2.3
    ...

Make sure you see a version at least 3.2.

*Install*

If you are on macOS, you can install MongoDB using [Homebrew](https://brew.sh). You will need to add the MongoDB tap following the
instructions [here](https://github.com/mongodb/homebrew-brew).

If you are on Linux, see the MongoDB documentation's [instructions](https://docs.mongodb.com/manual/administration/install-on-linux/).

*Setup*

You can get a MongoDB server up and running locally any number of ways.
Here is one:

1. Create a folder ``process_bigraph_work/mongodb``. This is where MongoDB will
   store the database We store the database here instead of at the
   default location in ``/usr/local/var/mongodb`` to avoid permissions
   issues if you are not running as an administrator.
2. Make a copy of the ``mongod`` configuration file so we can make
   changes:
 
       $ cp /usr/local/etc/mongod.conf process_bigraph_work/mongod.conf

   Note that your configuration file may be somewhere slightly
   different. Check the MongoDB documentation for your system.
3. In ``process_bigraph_work/mongod.conf`` change the path after ``dbPath:`` to
   point to ``process_bigraph_work/mongodb``.
4. Create a shell script ``process_bigraph_work/mongo.sh`` with the following
   content:

       #!/bin/bash

       mongod --config mongod.conf

5. Make the script executable:

        $ chmod 700 process_bigraph_work/mongo.sh

6. Now you can launch MongoDB by running this script:

        $ process_bigraph_work/mongo.sh
