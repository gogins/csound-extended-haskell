# csound-extended-haskell

Michael Gogins<br>
https://github.com/gogins<br>
http://michaelgogins.tumblr.com

## Introduction

This directory contains Haskell code that exposes the Csound shared 
library as a Haskell module, and provides an example of using that module.

The Csound module includes a `playCsound` function that renders a Euterpea 
Music object using Csound. This can be used with Euterpea, the Haskell School 
of Music, Kulitta, Jazzkell, and relatives.

## Changes

See https://github.com/gogins/csound-extended-haskell/commits/main for the 
commit log.

## License

This file is part of csound-extended-haskell.

This code is free software; you can redistribute it
and/or modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

csound-extended-haskell is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with Csound; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA
02110-1301 USA

## Installation

To install the Csound Haskell module, first you must install the Csound, then 
the Haskell platform, then install Euterpea. I advise also installing the 
Haskell School of Music, Kulitta, and Jazzkell.

To do this so that everything works can be tricky. A recent version of all 
software is advisable. Here is what worked for me. Before you carry out these 
steps, look at the Euterpea installation instructions and see if these  
instructions still make sense.

```
#!/bin/bash
# Remove any previous local installation of the Haskell platform.
cd
rm -rf .ghcup
rm -rf .ghc
rm -rf .cabal

# Download and install the current generic Linux installer for the Haskell 
# platform. Run the following command and do as it instructs to install 
# the Haskell platform locally (i.e. in your home directory).
curl https://get-ghcup.haskell.org -sSf | sh

# Obtain the latest version of installed Haskell packages.
cabal v2-update

# Install the following packages:
cabal install Euterpea --reinstall --force-reinstalls --allow-newer --lib
cabal install HSoM --reinstall --force-reinstalls --allow-newer --lib
cabal install Kulitta --reinstall --force-reinstalls --allow-newer --lib

# Clone the Jazzkell repository into your home directory and install the 
# current version of Jazzkell.
cd
git clone https://github.com/donya/Jazzkell.git
cd Jazzkell
cabal install --reinstall --force-reinstalls --allow-newer --lib

# Start up Timidity in the background as a synthesis server for Haskell.
timidity -iA -Os &
```
Test your installation by running a few examples, choosing the appropriate 
MIDI device for Timidity for Euterpea. The following tests the Haskell School 
of Music, the MUI graphical user interface library provided by Euterpea, and 
Euterpea itself:
```
mkg@bodhimandala:~/Kulitta/Examples$ ghci
GHCi, version 8.6.5: http://www.haskell.org/ghc/  :? for help
Prelude> import HSoM.Examples.MUIExamples2
Prelude HSoM.Examples.MUIExamples2> bifurcate
```
This tests Jazkell:
```
cd
cd Jazzkell/examples
mkg@bodhimandala:~/Jazzkell/examples$ ghci
GHCi, version 8.6.5: http://www.haskell.org/ghc/  :? for help
Prelude> :load SimpleBossa
[1 of 1] Compiling SimpleBossa      ( SimpleBossa.lhs, interpreted )
Ok, one module loaded.
*SimpleBossa> playDev 2 m
```

Finally, install the Csound module for Haskell:
```
cd
cd csound-extended/haskell
cabal install
```

To generate reference documentation, execute:
```
haddock Csound --html

