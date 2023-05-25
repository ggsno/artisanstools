# MSW

### 초기 설정 및 간단 예제

```bash
yarn add -D msw
npx msw init <PUBLIC_DIR>
```

```tsx
// /mock/index.ts

import { rest, setupWorker } from "msw";

const mockData = {
  data: ["hello"],
};

const mockApis = [
  rest.get(`/api/hello`, async (req, res, ctx) => {
    return res(ctx.json(mockData.data));
  }),
  rest.post(`/api/hello`, async (req, res, ctx) => {
    mockData.data.push(await req.json());
    return res(ctx.status(201));
  }),
];

export default function initMocks() {
  const worker = setupWorker(...mockApis);
  worker.start();
}
```

```tsx
// vite + react + typescript
// @/main.tsx

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import initMocks from "@/mock";

/** 개발모드 여부에 따라 실행 */
if (import.meta.env.DEV) initMocks();

ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
