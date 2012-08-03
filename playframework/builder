#!/bin/bash
set -e
BUILDROOT="$(dirname "$0")"
VERSION=2.0.3

echo 'Checking if Play framework is already installed...'
if [ -d ~/play-${VERSION} ]
then
    echo 'Play framework found.'
else
    echo 'Play framework not found. Installing it...'
    echo '- Download Play framework'
    curl -O http://download.playframework.org/releases/play-${VERSION}.zip
    if [ -e play-${VERSION}.zip ]
    then
        echo '- Unzip downloaded file'
        unzip -q play-${VERSION}.zip
        if [ -d play-${VERSION} ]
        then
            echo '- Copy play installation'
            cp -R ./play-${VERSION} ~/play-${VERSION}
            echo 'Play installed.'
        else
            echo 'Unzip failed !'
        fi
    else
        echo 'Download failed !'
    fi
fi

echo 'Installing application'
rm -rf ~/application
cp -R  ./$SERVICE_APPROOT ~/application

echo 'Symlinking application logs to Supervisor area...'
rm -rf ~/application/logs
ln -s /var/log/supervisor ~/application/logs

echo  'Installing run script...'
cp "$BUILDROOT/run" ~

echo 'Building the Play application'
cd ~/application

export _JAVA_OPTIONS="-Xms502m -Xmx502m"
echo ' -- Cleaning -- '
~/play-${VERSION}/play clean
echo ' -- Compiling -- '
~/play-${VERSION}/play compile
echo ' -- Staging -- '
~/play-${VERSION}/play stage

echo 'Build complete.'
