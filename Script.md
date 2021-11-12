###Prerequisites:

-gpg2 (Linux)
-kelopata/gpg4win (windows) - https://www.gpg4win.org/
-gnupg (Mac OS) - https://gpgtools.org/

.....................................................

###INTRO

Hello there travellers

If you are watching this video, it's most likely that you are interested in knowing whether or not you’re running the software intended by their authors.

Often you will hear the word safe used in terms of running a program. Please be aware that this is used in a relative sense, in the same way many other things in life can be considered safe, even though they're capable of causing harm.

With that out of the way, let's get on to the matter at hand; The GNU Privacy Guard (GPG).

GPG is a complete and free implementation of the OpenPGP standard that has been in circulation since 1997. 
What makes GPG Free Software is that it can be freely used, modified and distributed. I recommend taking a look at the GNU project and the Free Software Foundation. Their webpage, is pretty interesting and you'll find a lot more Free Software there - https://www.gnu.org/gnu/gnu.html
You can also learn more about the OpenPGP standard on the following wiki page - https://en.wikipedia.org/wiki/Pretty_Good_Privacy

GPG allows anyone to encrypt and sign their data and communications. You will typically be prompted to carry out some basic operations when handling monero related software so we thought it would be good to have an easy to follow guide.

If you haven't installed the software for your operating system already, please go ahead and do so. You'll find appropriate links in the description below.
Please be aware that most linux distros will have GPG installed already. If you find that you don't have it, please check your package manager and install it from there.

.....................................................

###CREATING YOUR OWN KEYS

Let's start by opening up a terminal window and checking which version of gpg we have installed.
Don't worry that i'm using ubuntu, this is relevant to all OS's, if you're a windows user, please open a powershell window.
Do take a look at the video description as most of the commands we’re going to use can be found there. Feel free to copy and paste along with this video.

Let's start by typing 'gpg --version' and pressing enter. If you're not familiar with using the command line, please remember, you need to hit enter each time for the terminal to read your input. 

If you weren't sure if you had it installed, this is a pretty good test. This command will print some interesting information, including the version, the licence, the home directory for gpg and the supported algorithms

Now we've confirmed that it's installed, we're going to create our very own set of keys.

keys typically come in pairs, a private key and a public key. In simple terms, a private key is one which you use to prove who you are and a public key is one which is used to tell other people who you are. 
It's a pretty simple system, but has deep roots in cryptography. if you're interested in reading a little more about the fundamentals, check out the link entitled 'How PGP Works' - https://users.ece.cmu.edu/~adrian/630-f04/PGP-intro.html

to generate our own set of keys we're going to use the command 'gpg --full-generate-key', don't forget to include the hyphens 

First it will ask you what kind of key you would like to create, for the purpose of this video we'll be using the default option 'RSA', so we'll select option 1.
next it will ask you about the level of encryption you require, the larger the number the more data is used to generate the keys. more data generally means more secure. we're going to choose 4096 bit because... why not
we will then be asked how long we want our keys to remain valid, this is a personal choice, because there is no limit to the number of keys one can generate and the fact i will not be hosting my keys publically, i'm going to choose 0, 'never expires'

yes, i'm sure

All keys are assigned user ids, they're typically made up of a name, comment and email address. For the purpose of this video, this name and email address could be quite literally anything. your own credentials can be a crazy as mine
Once we have entered all this information we're going to type 'o' for 'okay', but before we hit enter I want to warn those who like to use password generators. you're going to need to enter a new password in the next step.

Once we have entered and confirmed the password, we're going to generate some entropy, in other words, move the mouse and bash the keyboard a bit.

Now that we have generated our very own keypair, we can use the command 'gpg --list-keys' to verify it's existence.
What we have done simultaneously is added our keys to our very own keyring. 
key rings are a little outside the scope of this video, however it's important to know that they may be different and you can have as many as you like. as we won't be specifying, we're going to be working with a default keyring

you can have

.....................................................

###VERIFYING & IMPORTING SOMEONE ELSE'S PUBLIC KEY

To demonstrate we're going to head over to getmonero.org.
Click on the downloads tab and scroll down until you see the different files. At this point, download the file that suits you best, for me it's the linux version, if you’re using windows, grab the Installer version.
Now that it's downloaded we’ll need two bits of information. 

The first is located in the 'hashes.txt'. Hashes are unique identifiers that are generated from using a hashing algorithm. These algorithms use information about the file and because of that we can detect changes easily and quickly.
We're interested in making sure that the hash of the file we have downloaded matches the hash contained in this file.

I'm going to right click and 'save link as'. Let's take a look at what we've got here.

You guessed it, this text file contains the hashes for each release, but if you look at the heading and footer, you will notice that this actually comes in the form of a signed message.
This is important, because now we can see if these hashes were signed by someone we know.

The next piece of information we need is the public key for the person who supposedly signed these hashes. Which we can find via the getmonero site.

Let's take a look at the git source as recommended. Here we find the public key of 'binaryfate' one of the key contributors to the monero ecosystem. Feel free to check out his git profile and see what he's been working on.

Most keys will be suffixed with '.asc'. To download this key, right click on the link titled 'raw' and 'save link as'

Next, open your file explorer and navigate to the directory in which you save these files. If you haven't saved them to the same place, please move them now.

With the file explorer open, right click and select ‘open terminal here’. If you're a windows user, you will need to use 'shift+right click' and select open powershell here.

At this point we’re interested in taking a look at the fingerprint of binaryfates public key. Fingerprints are best thought of as summaries of the key.
We can view this fingerprint with the following command, 'gpg --keyid-format long --with-fingerprint binaryfate.asc'

Fingerprints are a useful way of making sure that the key you're importing, is actually the one you want. If you know the person whose key you are trying to import you can check it with them manually.
you will often find that a fingerprint will be hosted somewhere on the internet and you don't need to go through that manual process.

Please bear in mind, if a webpage or repo has been compromised and the fingerprint and the public key are located in the same place, the likelihood is that both were compromised, so checking the fingerprint is pretty much pointless. However, if the fingerprint and key are hosted in seperate locations, it's always worth checking.

In our case, we can find the fingerprint for binaryfates public key on the get monero web page. you can either click on this link here, or use the wwebpage we have provided below - https://www.getmonero.org/resources/user-guides/verification-allos-advanced.html

Click on the heading 'Verify and Import Signing Key', scroll down until you find this section 'Verify the fingerprint matches'. Now let's visually compare that to the one which is printed in our terminal window.
If you've got a match, great, if not, verify the web links you used and report your findings to the community.

Now that we have a little more confidence in the key we've downloaded we're going to use the command 'gpg --import binaryfate.asc'
Once again we can use 'gpg --list-keys' to verify that it has been added to our keyring

.....................................................

###SIGNING SOMEONE ELSE'S PUBLIC KEY

This step is a little unnecessary and is more relevant to public keyrings and the pgp ecosystem as a whole, namely the 'web of trust', which is totally outside the scope of this video, but you can learn more about the web of trust through the p2p foundation - https://wiki.p2pfoundation.net/Web_of_Trust
For us, going through this step means that you have a more simple log when you verify signatures in the future.

It is possible to add this level of trust to the signature you have imported with the '--edit-key' flag. 
In our case we will use the command 'gpg --edit-key binaryfate@getmonero.org'
Once GPG is running you will see 'gpg>', you now have a few options including the ability to sign it with your own key, type ‘help’ to find out what else you can do.
For now, let’s type 'sign', confirm with 'y' and now enter the password you set up in the previous step.

All done

Now use 'ctrl+c' to exit gpg

.....................................................

###VERIFYING SIGNATURES & HASHES

Everything we've done so far has now given us the ability to verify the signature on the hash file we downloaded earlier.

The next command we're going to use is 'gpg --verify hashes.txt', if you're typing this out yourself, remember that you can use 'tab' to autocomplete.

If everything has gone to plan, we should see a message stating 'Good signature from "binaryFate <binaryfate@getmonero.org>"'

If you don't receive this message, please follow the procedure recommended upon failed fingerprint verification

GREAT!

Now we can compare the hashes in the text file to those of the file we downloaded.

If you're using linux you can use the command 'sha256sum --check hashes.txt', we're going to look for the version we downloaded and check to see if everything is 'OK'

If you're using windows, please use the command 'Get-Filehash' and then the name of the file you downloaded. Manually compare this hash to the one in the hashes.txt file

Now we know, the software that we have is the one intended by the person who signed these hashes!

.....................................................

###OUTRO

PGP relies heavily on trust, it's for that reason you should be sure that the public key you have in your keyring is in fact trustworthy.

If you’re not, then you may as well skip this step and accept the consequences. That being said, checking the piece of software you download by verifying them against signed hashes is best practice.

The instructions in this video will be relevant to a lot of our other videos so please make yourself familiar.

Anyway, that's it for this installment, peace be with you privacy fans.
