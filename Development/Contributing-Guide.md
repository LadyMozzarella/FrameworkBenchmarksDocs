The community has consistently helped in making these tests better, and we welcome any 
and all changes. These guidelines prevent us from having to give repeated feedback on 
the same topics: 

* **Use specific versions**: If you're updating any software or dependency, please be 
specific with the version number. Also, update the appropriate `README` to reflect 
that change. Don't rely on the package manager to deliver a specific version, apt 
consistently returns different versions on Ubuntu 12.04 vs 14.04.
* **Rope in experts**: If you're making a performance tweak, our team may not be 
able to verify your code--we are not experts in every language. It's always helpful 
to ping expert users and provide a basic introduction on their credentials. If you 
are an expert that is willing to be pinged occasionally, please add yourself to 
the appropriate test README files. 
* **Use a personal Travis-CI account**: This one is mainly for your own sanity. Our 
[main Travis-CI](https://travis-ci.org/TechEmpower/FrameworkBenchmarks) can occasionally
become clogged with so many pull requests that it takes a day to finish all the 
builds. If you create a fork and enable Travis-CI.org, you will get your own 
build queue. This means 1) only your commits/branches are being verified, so there is 
no delay waiting for an unrelated pull request, and 2) you can cancel unneeded items. 
This does not affect our own Travis-CI setup at all - any commits added to a pull 
request will be verifed as normal. 
* **Read the README**: We know that's cliche. However, our toolset drags in a lot of 
different concepts and frameworks, and it can really help to read the README's, such 
as this one, the one inside the `toolset/` directory, and the ones inside specific 
framework directories
* **Use the Development Virtual Machine**: Our Vagrant scripts can setup a VM for you
that looks nearly identical to our test environment. This is even better than relying
on the Travis-CI verification, and you are strongly encouraged to use this. See 
the [deployment directory](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment) for specifics

---