**THIS IS A TEST VERSION OF THE INTRINSIC COIN WALLET. THE CODE HAS HARD CODED PATH FILES. THIS WILL CHANGE ONCE THE ISSUES WITH THE RESOURCES.QRC FILE ARE RESOLVED**

Dependencies: boost >= 1.58, CMake >= 2.8.6, GCC >=4.7.3, Qt >=5.0

**1. Clone wallet sources**

```
git clone https://github.com/intrinsiccoin/IntrinsicCoin-GUI-Wallet.git
```

**2. Update git submodule:**

```
git submodule update --init --recursive
git submodule foreach git pull origin master
```

**3. Build**

#### Windows build

On windows, you will have to first seperately build rocksdb and IntrinsicCoin projects with -DSTATIC=0 option. Now pick the .lib files from the built project into the /libs folder in the root or source directory. Then you can proceed with cmake of GUI wallet and build using the following commands.

```
mkdir build && cd build && cmake -G "Visual Studio 15 Win64" .. && make
```

On windows, you may find it helpful to explicitly include Boost and Qt library paths:

```
cmake -G "Visual Studio 15 Win64" -DCMAKE_PREFIX_PATH="C:\Qt2\5.9.1\msvc2015" -DBOOST_ROOT="C:\boost_1_64_0_built" -DBOOST_INCLUDEDIR="C:/boost_1_64_0_built/lib32-msvc-14.1" -DBOOST_LIBRARYDIR="C:\boost_1_64_0_built\libs"
 ```
#### *nix build
```
mkdir build && cd build && cmake -DSTATIC=1 .. && make
```

**The details below are from one of the issues on github (https://github.com/forknote/forknote/issues/1)**

You can look at my repo for windows ONLY GUI wallet. The build is not straightforward though, unfortunately.

Do the following:

    Fork the IntrinsicCoin-GUI-Wallet repository, add the submodule in your clone or just replace the 'IntrinsicCoin' folder with your coin code.
    BEFORE building the wallet you need to do the following:
    a. Delete the contents of the 'libs' folder within the GUI wallet root directory.
    b. In the IntrinsicCoin-GUI-Wallet/IntrinsicCoin/External folder create a 'Build' folder, execute cmake with DSTATIC option 0. This step is important.
    c. Build in MSVCS 2017/Boost 1.66, then copy the resulting rocksdblib.lib file from the 'Build' folder into the 'libs' folder within the GUI wallet root directory.
    d. Next, Build the 'IntrinsicCoin' using cmake with DSTATIC option 0. Again, this step is important. Note: The build in MSVC 2017 may fail but dont worry, just copy the resulting '.lib' files from your coin's build folder into the 'libs' folder within the GUI wallet root directory.
    c. Next get into the GUI wallet root directory, ie 'IntrinsicCoin-GUI-Wallet' and do cmake with DSTATIC option 1, and build your wallet. Hopefully you will see the 'IntrinsicCoinWallet.exe' file your build folder.
    Now go ahead and try out your wallet.

So in short, this is a crude/tricky way to get your code working on Windows. But credit is due to @jasin. Thanks for his efforts, this wallet was possible.

But its way too easy to get your coin a GUI wallet for Ubuntu. Fork the ChavezCoinWallet code, put your coin's code in the 'cryptonote' folder and execute cmake/make. Voila, your wallet is ready. Its pretty straightforward. Hope this helps in your first trial and error.
