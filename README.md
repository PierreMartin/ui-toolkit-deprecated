## 📦 Install

```bash
npm i
npm start
open http://localhost:8001/components
```

- VOIR exemple dans BO, branche work/PMA/POC/toolkit, fichier => backorga/routes/events/eventconfig/antdtest/index.tsx (faire un npm link antd)

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

## 📦 Link to a repo

```bash
npm run compile
npm run dist
npm link (or npm publish)
```

## 🔨 Full exemple :

```jsx
import * as React from 'react';
import { Form, Input, Button, Select } from 'antd';
import './reset-old-shared.less';

const { Option } = Select;
const FormItem = Form.Item;

const layout = {
  // labelCol: { span: 8 },
  // wrapperCol: { span: 16 }
};
const tailLayout = {
  // wrapperCol: { offset: 8, span: 16 }
};

interface IDemo {
  entityValues: any;
  i18n?: any;
}

export const Demo = ({ i18n, entityValues }: IDemo) => {
  const [form] = Form.useForm();
  const [fieldsTyping, setFieldsTyping] = React.useState({});
  const required = i18n.translate('fieldvalidation.required');

  // Set required errors here :
  React.useEffect(() => {
    // eslint-disable-next-line no-restricted-syntax
    for (const key in entityValues) {
      if (Object.prototype.hasOwnProperty.call(entityValues, key)) {
        if (!entityValues[key]) {
          form.setFields([{ name: key, errors: [required] }]);
        }
      }
    }
  }, []);

  const onSubmit = (values: any) => {
    console.log('onSubmit => ', values);
  }; // Use it ONLY IF a submit button is in this <From>

  const onValuesChange = (field: any) => setFieldsTyping({ ...fieldsTyping, ...field });

  const onGenderChange = (value: string) => {
    switch (value) {
      case 'male':
        form.setFieldsValue({ note: 'Hi, man!' });
        break;
      case 'female':
        form.setFieldsValue({ note: 'Hi, lady!' });
        break;
      case 'other':
        form.setFieldsValue({ note: 'Hi there!' });
        break;
      default:
        break;
    }
  };

  const onReset = () => {
    form.resetFields();
  };

  const onFill = () => {
    form.setFieldsValue({
      note: 'Hello world!',
      gender: 'male',
    });
  };

  console.log('fieldsTyping ======> ', fieldsTyping);

  return (
    <Form
      {...layout}
      name="basic-form"
      form={form}
      layout="vertical"
      initialValues={{
        note: '', // Defaults values here
      }}
      onValuesChange={onValuesChange}
      onFinish={onSubmit}
      scrollToFirstError
    >
      <FormItem
        name="note"
        label="Note"
        rules={[
          {
            required: true,
            message: required,
          },
        ]}
      >
        <Input placeholder="Enter a note" />
      </FormItem>

      <FormItem
        name="email"
        label="Email"
        rules={[
          {
            type: 'email',
            message: i18n.translate('email.invalid'),
          },
          {
            required: true,
            message: required,
          },
        ]}
      >
        <Input prefix={<i className="inwink-email" />} placeholder="E-mail" />
      </FormItem>

      <FormItem
        name="password"
        label="Password"
        rules={[
          {
            required: true,
            message: 'Please input your password!',
          },
          {
            pattern: new RegExp(/^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[0-9a-zA-Z]{6,}$/),
            // eslint-disable-next-line max-len
            message:
              'Password must be minimum 6 characters and contain at least one lowercase letter, uppercase letter number and no special characters',
          },
        ]}
        hasFeedback
      >
        <Input.Password prefix={<i className="inwink-lock" />} placeholder="Password" />
      </FormItem>

      <FormItem name="gender" label="Gender" rules={[{ required: true }]}>
        <Select
          placeholder="Select a option and change input text above"
          onChange={onGenderChange}
          allowClear
        >
          <Option value="male">male</Option>
          <Option value="female">female</Option>
          <Option value="other">other</Option>
        </Select>
      </FormItem>

      <FormItem
        noStyle
        shouldUpdate={(prevValues, currentValues) => prevValues.gender !== currentValues.gender}
      >
        {({ getFieldValue }) =>
          getFieldValue('gender') === 'other' ? (
            <FormItem name="customizeGender" label="Customize Gender" rules={[{ required: true }]}>
              <Input />
            </FormItem>
          ) : null
        }
      </FormItem>

      <FormItem {...tailLayout}>
        <Button type="primary" htmlType="submit">
          Submit
        </Button>
        <Button htmlType="button" onClick={onReset}>
          Reset
        </Button>
        <Button type="link" htmlType="button" onClick={onFill}>
          Fill form
        </Button>
      </FormItem>
    </Form>
  );
};
```
