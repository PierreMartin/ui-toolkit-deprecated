## 📦 Install

```bash
npm install antd
```

```bash
yarn add antd
```

## 🔨 Usage

```jsx
import { Button, DatePicker } from 'antd';
import 'antd/dist/antd.css';

const App = () => (
  <>
    <Button type="primary">PRESS ME</Button>
    <DatePicker placeholder="select date" />
  </>
);
```

And import style manually:

```jsx
import 'antd/dist/antd.css'; // or 'antd/dist/antd.less'
```

```bash
npm run compile
npm run dist
npm link (or npm publish)
```
