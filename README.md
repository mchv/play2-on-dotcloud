# Customizable Play! 2 service for dotCloud

This is an implementation of the [dotCloud](http://www.dotcloud.com/) [java service](http://docs.dotcloud.com/services/java/), using the new custom build API.

## What?

You want this if:

- you use dotCloud
- you deploy Play! 2 apps

## How?

To test this, use the good old "git clone / dotcloud push" method:

    git clone git://github.com/mchv/play2-on-dotcloud.git
    dotcloud push plop play2-on-dotcloud

To deploy your own application, put it code source to application

Don't forget to do one of the following:

- ``dotcloud push`` with the ``--all`` flag (will force the use of rsync over git),
- rm the ``.git`` directory (the CLI will gracefully fallback on rsync).

## Troubleshooting

If it doesn't work, try ``dotcloud logs`` to see what's happening.

## Scaling

Horizontal scaling will work as expected. If you apply vertical scaling, you should probably edit ``jetty/run`` to customize the JVM parameters and specify an appropriate heap size.

## Warning

This recipe is based on dotCloud "custom build API" and is a work in progress
