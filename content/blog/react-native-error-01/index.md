---

title: ERROR NOTE 

date: "2021-03-11"

tags: [error,react-native]

description:  npm run ios 실행 후 error 발생

---

```
npm run ios
실행시 error 발생
```



```
** BUILD FAILED **

The following build commands failed:
        CompileC /Users/jangjaewon/Library/Developer/Xcode/DerivedData/foodDelivery-dvriqngjhvwindghtqghlmixgxxm/Build/Intermediates.noindex/foodDelivery.build/Debug-iphonesimulator/foodDelivery.build/Objects-normal/x86_64/main.o /Users/jangjaewon/Desktop/app/foodDelivery/ios/foodDelivery/main.m normal x86_64 objective-c com.apple.compilers.llvm.clang.1_0.compiler
        CompileC /Users/jangjaewon/Library/Developer/Xcode/DerivedData/foodDelivery-dvriqngjhvwindghtqghlmixgxxm/Build/Intermediates.noindex/foodDelivery.build/Debug-iphonesimulator/foodDelivery.build/Objects-normal/x86_64/AppDelegate.o /Users/jangjaewon/Desktop/app/foodDelivery/ios/foodDelivery/AppDelegate.m normal x86_64 objective-c com.apple.compilers.llvm.clang.1_0.compiler
(2 failures)
```

문제 해결

```
cd ios //디렉토리 이동
pod update
npm run ios
```

