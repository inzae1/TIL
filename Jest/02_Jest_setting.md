

# Jest setting

#### **Jest jest.config.js** 

- `root` 폴더에 `jest.config.js`를 만들고 상기 내용을 넣는다

```javascript
module.exports = {
  moduleFileExtensions: ["js", "json", "jsx", "ts", "tsx", "json"],
  transform: {
    "^.+\\.(js|jsx)?$": "babel-jest",
  },
  moduleNameMapper: {
    "^@/(.*)$": "<rootDir>/$1",
    '\\.(jpg|ico|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$':
      '<rootDir>/__mocks__/fileMock.js',
    '\\.(css|less)$': '<rootDir>/__mocks__/fileMock.js',
  },
  testMatch: [
    "<rootDir>/**/*.test.(js|jsx|ts|tsx)",
    "<rootDir>/(tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx))",
  ],
  transformIgnorePatterns: ["<rootDir>/node_modules/"],
};
```

- `moduleFileExtensions`, `moduleNameMapper`, `testMatch` 는 테스트를 적용할 파일들을 설정한다.

- `moduleNameMapper` 를 통해 특정 파일명을 가진 리소스들은 `fileMock.js`로 대체하였다.
- `transform`은 babel 처리를 설정한다.
- `transformIgnorePatterns` 는 test 제외 대상을 설정한다.


#### **fileMock.js** 

```javascript
module.exports = '';
```
- 이미지나 음원 파일을 통해 확인하는 일은 없으니, 빈 문자열을 export 한다.

#### **babel.config.js**

```javascript
module.exports = {
  presets: [
    [
      "@babel/preset-env",
      {
        targets: {
          node: "current",
        },
      },
    ],
  ],
};
```

- 루트 폴더에 `babel.config.js` 를 만들고 상기 내용을 적는다.
- 바벨 적용시 preset을 적용할 수 있도록 설정한다.

#### **package.json**

```javascript
"scripts": {
    "test": "jest",
  },
```
- `package.json` 에 test 실행시 jest 가 실행되도록 작성한다.