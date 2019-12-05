dva
```js
// 2. Model
app.model({
  namespace: 'count',
  state: 0,
  reducers: {
    add(state) { return state + 1 },
  },
  effects: {
    *addAsync(action, { call, put }) {
      yield call(delay, 1000);
      yield put({ type: 'add' });
    },
  },
});

```

ramatch
```js
const count = {
  state: 0,
  reducers: {
    add: state => state + 1,
  },
  effects: (dispatch) => ({
    async addAsync() {
      await sleep(() => {
         dispatch.count.add()
      }, 1000)
    }
  }),
}
```

biz-store
```js
class CountAction extends BaseState {
    initState() {
        this.init(Map({count: 0}))
    }
    add() {
        this.update('count', (count)=>count+1);
    }
    async addAsync() {
        const me=this;
        await sleep(() => {
            me.add();
        }, 1000)
    }
}
export default new CountAction('count')
```

表单
```js
import {Form,Input} form 'form';

class FormDemo extends Component{
    state = {
        value: {
            name: '',
        },
    }
    onFormChange = (value) => {
        this.setState({
            value,
        });
    }
    onFormSubmit = () => {
        // console.log('submit')
    }
    render() {
        const me = this;
        const {
            value,
        } = me.state;
        return (
            <Form
                value={value}
                enableDomCache={false}
                onChange={me.onFormChange}
                onSubmit={me.onFormSubmit}
            >
                <div className="container">
                    <input
                        className="biz-input"
                        data-name="name"
                        data-rules={[{ max: 10, message: '最大长度10' }]}
                        type="text"
                    />
                    <Button type="primary" htmlType="submit">提交</Button>
                </div>
            </Form>
        )
    }
}
```
