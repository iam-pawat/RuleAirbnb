<b> กฏ Eslint React และ Airbnb JavaScript Style Guide </b>

<b> วิธีติดตั้ง </b>

1. ติดตั้ง dependency 2 ตัวนี้
> yarn add eslint eslint-loader --dev
<hr>
2. ทำการ generate roles ที่จะใช้

> eslint --init 
<hr>
3. เลือกคำตอบดังนี้
  
  3.1 ผมจะเลือกใช้กฏตามมาตฐานสากลของ Airbnb จึงเลือกข้อ 2
  > Use a popular syle guide
  
  3.2 เลือก Style Guide ของ Airbnb
  > Airbnb
  
  3.3 ใช้ React 
  > y
  
  3.4 เลือกใช้ file config ที่เป็น json
  > JSON
<hr>
4. รอสักครู่...  จะได้ไฟล์ชื่อ.eslintrc.json
<pre>
// .eslintrc.json
  {
    "extends": "airbnb"
  }
</pre>
<hr>
5. ให้เพิ่มตัว loader ด้านล่างเพื่อให้ babel และ eslint ไปอ่านไฟล์ .js ใน webpack.dev.config.js

<pre> 
//webpack.dev.config.js หรือ webpack.config.js
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: ['babel-loader', 'eslint-loader'],
      },
    ],
  },
</pre>

6. จากนั้นพอลอง > yarn start จะพบ error เช่น
<pre>
 D:\springboots\true\tsm-payment-web\reactjs\Index.js
   3:1   error  Expected indentation of 0 spaces but found 8   indent
   8:16  error  'document' is not defined                      no-undef
  12:22  error  'window' is not defined                        no-undef
  15:3   error  JSX not allowed in files with extension '.js'  react/jsx-filename-extension

</pre>

7. วิธี Merge eslint กับ ide เนื่องจากผมใช้ intellij , webstorm จึงจะสาธิตตัว ide ตัวนี้นะ

 7.1 ให้กด ctrl+alt+s
 
 7.2 เลือกที่ 
 <pre>
  Language & Frameworks > Javascript > Code Quality Tools > ESLint 
  
  กด Enable > OK
 </pre>
 
8. จากนั้นไปที่ไฟล์ที่ Error  
  > D:\springboots\true\tsm-payment-web\reactjs\Index.js
  
9. ให้เอาเมาส์ไปชี้ที่ Error เราจะเห็นเป็นขีดแดงๆ ให้เลือก > ESlint: Fix Current File  ตัว ide จะทำการแก้ Code อัตโนมัติตาม Style Guide ที่เราเลือก
<hr/>
10. Error บางอย่างเช่น 

<pre>
  8:16  error  'document' is not defined                      no-undef
  12:22  error  'window' is not defined                        no-undef
  15:3   error  JSX not allowed in files with extension '.js'  react/jsx-filename-extension
 </pre>
 
 เราสามารถ Allow ให้ผ่านกฏได้โดยการ config ไฟล์ .eslintrc.json ซึ่งดูได้จากไฟล์ ที่เอาแนบมาให้นำไปใช้เลยก็ได้
 หรือบางทีถ้าหาวิธีแก้ Error ไม่ได้ให้ไปอ่านตามนี้คับเป็น Official จะบอกวิธีแก้ยังไงให้ถูก
 
 > https://github.com/airbnb/javascript
 
 <hr>
 
<b> ส่วนนี้จะเป็นส่วนที่ผมได้รวบรวมวิธีแก้เอาไว้ </b>

<h2>1. Unexpected dangling '_' in '__INITIAL_STATE__'                               no-underscore-dangle 

</h2>

วิธีแก้ 
ให้นำ
> /* eslint no-underscore-dangle: 0 */

ไปวางบนบรรทัดที่เราใช้ _
 
<h2>2. error  JSX not allowed in files with extension '.js'  react/jsx-filename-extension

</h2>
วิธีแก้
ให้นำ 
<pre> 

    "rules": {
        "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]
    }

</pre>

ไปวางในไฟล์ config ของ ESlint

<h2>3. error  'document' is not defined                      no-undef
   error  'window' is not defined                        no-undef
  
</h2>
 วิธีแก้
 ให้นำ
 
 <pre>
 
    "env": {
        "browser": true,
        "node": true
    }
 
 </pre>
 
 ไปวางในไฟล์ config ของ ESlint
 
<h2> 4. error  Parsing error: Unexpected character '@'

</h2>
วิธีแก้

ให้เพิ่ม dependency ดังนี้ 

> yarn add babel-eslint --dev

จากนั้นเอา

<pre>

"parser": "babel-eslint",

</pre>

ไปเพิ่มในไฟล์ config ของ ESlint
