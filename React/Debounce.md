# Debounce  
## Debounce để làm gì?  
- Tăng hiệu suất, performance của app, giảm thiêu số lần xử lí sự kiện hoặc call API
- Debounce function buộc 1 hàm phải đợi 1 thời gian nhất định trước khi nó được chạy lại
## Ý tưởng tạo 1 debounce  
- Ban đầu không có timeout
- Nếu chưa hết thời gian timeout mà hàm được gọi, xóa current timeout và reset timeout
- Nếu hết thời gian timeout hàm được gọi, thực thi hàm
## Ví dụ
### Ví dụ về input search
Không dùng debounce, việc call API search sẽ thực hiện mỗi lần người dùng onChange input  
```javascript
export default function App() {
  const [value, setValue] = useState(null);
  const doSearch = (value) => {
    // call API search
    // .....
    console.log("do search");
  };
  const handleChange = (e) => {
    setValue(e.target.value);
    doSearch;
  };
  return (
    <div className="App">
      <input type="text" name="name" onChange={handleChange} value={value} />
    </div>
  );
}
```  
Sử dụng debounce với lodash
```javascript
export default function App() {
  const [value, setValue] = useState(null);
  const doSearch = (value) => {
    // call API search
    // .....
    console.log("do search");
  };
  const debounceDoSearch = useCallback(_.debounce(doSearch, 1000), []);
  const handleChange = (e) => {
    setValue(e.target.value);
    debounceDoSearch(value);
  };
  return (
    <div className="App">
      <input type="text" name="name" onChange={handleChange} value={value} />
    </div>
  );
}
```  
Sử dụng debounce vứi useRef  
```javascript
export default function App() {
  const [value, setValue] = useState(null);
  const timeoutRef = useRef(null);
  const doSearch = (value) => {
    // call API search
    // .....
    console.log("do search");
  };
  const handleChange = (e) => {
    setValue(e.target.value);
    if (timeoutRef.current) clearTimeout(timeoutRef.current);
    timeoutRef.current = setTimeout(() => {
      doSearch(value);
    }, 3000);
  };
  return (
    <div className="App">
      <input type="text" name="name" onChange={handleChange} value={value} />
    </div>
  );
}
```



