대부분의 nextjs프로젝트 생성을 
`npx create-next-app@latest`
`tailwinscss option 'Yes'`
로 초기화를 하였는데 flowbite-react를 적용하려 하다보니 version관련 error가 발생한다.
해결책은,
### tailwindcss를 설치하지 않고
`npx create-next-app@latest` 
`tailwinscss option 'No'` 

### nexjs설치가 완료되면 tailwindcss를 수동으로 설치
`npm i tailwindcss` 

### flowbite-react를 설치하며 init옵션을 주면 관련 파일들을 생성, 패치한다.
`npx flowbite-react@latest init`

### 이후 react 컴포넌트에서 import 하여 사용
`import { Button } from "flowbite-react";`