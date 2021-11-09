1.  git show aefea
    commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
    Update CHANGELOG.md
    
2.  git show 85024d3
    commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)

3.  git show b8d720
    Merge: 56cd7859e05c36c06b56d013b55a252d0bb7e158
    Merge: 9ea88f22fc6269854151c571162c5bcf958bee2b
    
4.  git show v0.12.23
    commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
    
    git show v0.12.24
    commit 33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24)
    
    git show 85024d3100126de36331c6982bfaac02cdab9e76..33ff1c03bb960b332be3af2e333462dde88b279e --pretty=format:"Хэш:%H%nКоммментарий:%s%n" -s
    
   Хэш:33ff1c03bb960b332be3af2e333462dde88b279e
   Коммментарий:v0.12.24

   Хэш:b14b74c4939dcab573326f4e3ee2a62e23e12f89
   Коммментарий:[Website] vmc provider links

   Хэш:3f235065b9347a758efadc92295b540ee0a5e26e
   Коммментарий:Update CHANGELOG.md

   Хэш:6ae64e247b332925b872447e9ce869657281c2bf
   Коммментарий:registry: Fix panic when server is unreachable

   Хэш:5c619ca1baf2e21a155fcdb4c264cc9e24a2a353
   Коммментарий:website: Remove links to the getting started guide's old location

   Хэш:06275647e2b53d97d4f0a19a0fec11f6d69820b5
   Коммментарий:Update CHANGELOG.md

   Хэш:d5f9411f5108260320064349b757f55c09bc4b80
   Коммментарий:command: Fix bug when using terraform login on Windows

   Хэш:4b6d06cc5dcb78af637bbb19c198faff37a066ed
   Коммментарий:Update CHANGELOG.md

5.  git log -S "func providerSource" --reverse --oneline
    8c928e835 main: Consult local directories as potential mirrors of providers

6.  git log -L:globalPluginDirs:plugins.go -s --oneline
    78b122055 Remove config.go and update things using its aliases
    52dbf9483 keep .terraform.d/plugins for discovery
    41ab0aef7 Add missing OS_ARCH dir to global plugin paths
    66ebff90c move some more plugin search path logic to command
    8364383c3 Push plugin discovery down into command package
    
7.  git log -S "synchronizedWriters"
    Author: Martin Atkins <mart@degeneration.co.uk>
