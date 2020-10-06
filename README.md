# React Component Styling
- `yarn create react-app <project name>` 으로 리액트 앱 생성.
- `yarn start`로 로컬서버 실행. 
- `yarn add node-sass` 로 sass 컴파일러 설치

## sass-loader설정 커스터마이징
1. 모든 내용 커밋 후 `yarn eject`명령 실행.
1. config디렉토리 생성되며 내부에 webpack.config.js 파일 열기.
1. `sassRegex` 검색하기.
1. 2번째 검색결과에 아래와 같이 수정 후 서버 재실행.
```javascript 1.5
{
    test: sassRegex,
    exclude: sassModuleRegex,
    use: getStyleLoaders({
        importLoaders: 3,
        sourceMap: isEnvProduction && shouldUseSourceMap,
    }).concat({
        loader: require.resolve('sass-loader'),
        options: {
            sassOptions: {
                includePaths: [paths.appSrc + '/styles']
            },
            sourceMap: isEnvProduction && shouldUseSourceMap,
        }
    }),
    sideEffects: true,
},
```
- 만약 설정 변경 후 서버 재실행이 안된다면 node_modules 디렉토리 삭제 후   
`yarn install`후에 다시 실행할 것.

- 만약 utils.scss파일을 모든 scss에서 import한다면 webpack.config.js에 아래 구문 추가
```javascript 1.5
...

loader: require.resolve('sass-loader'),
            ...

            sourceMap: isEnvProduction && shouldUseSourceMap,
            //이부분 추가
            prependData: `@import 'utils';`
        }
```