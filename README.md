


main.cpp

l 1282 block reward int64 nSubsidy = 49 * COIN + 95 * CENT;

l1380    // debug print every 60 sec
if (GetAdjustedTime() > iDebugPrintSpacing + 59)
{
iDebugPrintSpacing = GetAdjustedTime();

printf("Difficulty before retarget %f. Difficulty after retarget %f\n",Difficulty(pindexLast->nBits),Difficulty(bnNew.GetCompact()));
if (pblock->nTime > pindexLast->nTime + nTargetSpacing*2)
{
printf("Working on current block %" PRI64d" sec. target spacing %" PRI64d" sec.\n", pblock->nTime - pindexLast->nTime, nTargetSpacing);
printf("Difficulty after reset %f\n",Difficulty(Params().ProofOfWorkLimit().GetCompact()));

l 1396
double Difficulty(unsigned int bnDiff)
{
int nShift = (bnDiff >> 24) & 0xff;
double dDiff =
(double)0x0000ffff / (double)(bnDiff & 0x00ffffff);
while (nShift < 29)
{
dDiff *= 256.0;
nShift++;
}
while (nShift > 29)
{
dDiff /= 256.0;
nShift--;
}
return dDiff;
}

chainparams l 36 nDefaultPort = 17711;

const char* pszTimestamp = "Eva Coin is named after talkshow host Eva Jinek";
genesis.nTime    = 1494888013;
genesis.nNonce   = 2087385161;
assert(hashGenesisBlock == uint256("0x000000006d7e2bfc108eb0bdfa44f01a55770449166215980d13c32563fb34a5"));
assert(genesis.hashMerkleRoot == uint256("0x1c70dcd890f673e76970c2de7125723d19eb8ffcc527cf861f6e19fec1741bb8"));

notEvilDime integration/staging tree
================================

http://hss3uro2hsxfogfq.onion

Copyright (c) 2017 notEvilDime Developers

What is notEvilDime?
----------------

notEvilDime is an experimental new digital currency that enables instant payments to
anyone, anywhere in the world. notEvilDime uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. notEvilDime is also the name of the open source
software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the notEvilDime client software, see http://hss3uro2hsxfogfq.onion

License
-------

notEvilDime is released under the terms of the MIT license. See `COPYING` for more
information or see http://opensource.org/licenses/MIT.

Development process
-------------------

Developers work in their own trees, then submit pull requests when they think
their feature or bug fix is ready.

If it is a simple/trivial/non-controversial change, then one of the notEvilDime
development team members simply pulls it.

If it is a *more complicated or potentially controversial* change, then the patch
submitter will be asked to start a discussion (if they haven't already) on the
[mailing list](http://sourceforge.net/mailarchive/forum.php?forum_name=notevildime-development).

The patch will be accepted if there is broad consensus that it is a good thing.
Developers should expect to rework and resubmit patches if the code doesn't
match the project's coding conventions (see `doc/coding.md`) or are
controversial.

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/notevildime/notevildime/tags) are created
regularly to indicate new official, stable release versions of notEvilDime.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test. Please be patient and help out, and
remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code.

Unit tests for the core code are in `src/test/`. To compile and run them:

    cd src; make -f makefile.unix test

Unit tests for the GUI code are in `src/qt/test/`. To compile and run them:

    qmake BITCOIN_QT_TEST=1 -o Makefile.test notevildime-qt.pro
    make -f Makefile.test
    ./notevildime-qt_test

Every pull request is built for both Windows and Linux on a dedicated server,
and unit and sanity tests are automatically run.
