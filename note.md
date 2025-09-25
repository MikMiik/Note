npm create vite@latest . -- --template react
npm install
npm install -g npm-check-updates
Remove-Item -Recurse -Force .git (rm -r -fo .git)
1. Chức năng của {}
  - Chèn expression
  - không chèn statement
  - không dùng if-else nhưng dùng ternary
  - chèn thuộc tính đối tượng
  - chèn src ảnh vào thẻ img
2. Lỗi eslint do chưa định nghĩa prop types
  - cần npm install prop-types
  MainContent.propTypes = {
    image: PropTypes.string.isRequired,
    title: PropTypes.string.isRequired,
    desc: PropTypes.string,
  }
3. Destructuring code
  ![alt text](image.png)
4. npm
  - Hệ thống quản lý gói (package manager) dành cho môi trường Node.js. Đây là công cụ chủ yếu dùng để cài đặt, 
quản lý và chia sẻ các thư viện JavaScript cũng như các module hỗ trợ phát triển ứng dụng web hoặc server-side
  - 2 cách cài: 
  + Project scope: cài vào project hiện tại
  + global scope: cài vào user
5. npx
  - Hỗ trợ các thư viện cung cấp file bin
  + khi tải 1 thư viện nào đó, file bin của thư viện sẽ được lưu vào thư mục bin của node-modules và npx sẽ tìm đến để thực thi (nếu có)
  + nếu tìm file bin của 1 thư viện mà chưa cài thư viện đó, npx sẽ tự động lên npm để cài thư viện, thực thi file bin rồi xóa thư viện
  -> tránh việc phải cài thư viện không cần thiết mà vẫn có thể thực hiện lệnh
6. yarn
  - tương tự npm nhưng có 1 số điểm khác, cụ thể ở https://www.sitepoint.com/yarn-vs-npm/ 
  - yarn cũng là 1 thư viện của npm, để cài yarn: npm install -g yarn (tương tự như lên edge để cài chrome)
7. devDependencies & dependencies
  - Các dependencies nói chung thể hiện các thư viện mà project phụ thuộc vào để có thể chạy code
  - devDependencies: là những thư viện dùng cho dev 
  - dependencies: là những thư viện dùng cho cả dev và production
8. file bin
  - khi một thư viện cung cấp file bin, điều đó có nghĩa là nó cung cấp một lệnh (command) mà bạn có thể chạy từ dòng lệnh (terminal)
  VD: khi cài create-react-app có thể chạy trực tiếp câu lệnh như create-react-app --help ngay trong terminal
  - khi gỡ thư viện cũng gỡ file bin
9. nanoid: thư viện giúp tạo id random
10. package-lock.json & package.json
  https://chatgpt.com/c/67f52fd8-1f2c-8010-93a8-93b86e5290e0
11. node-modules: chưa các thư viện được cài đặt trong project
12. public: gồm các file có thể truy cấp trực tiếp qua đường dẫn trên trình duyệt
--------------------------useEffect--------------------
13. useEffect(callback) (ít dùng)
  - gọi callback mỗi khi component re-render
  - gọi callback sau khi component thêm element vào DOM (kể cả khi callback viết trước lệnh return element trong DOM), thực tế code vẫn được
đọc theo trình tự, nếu useEffect được viết trước return thì các lệnh khác trong useEffect vẫn được thực hiện trước nhưng callback sẽ tạm thời được giữ lại,
đợi đến khi các element được tạo trong DOM mới thực hiện callback
14. useEffect(callback, [])
  - nếu fetch API bên ngoài mà không cho vào useEffect thì mỗi lần useState API sẽ bị call lại, nếu cho vào callback useEffect(callback) thì bị gọi lại
mỗi lần component re-render -> sinh ra useEffect(callback, [])
  - chỉ gọi callback một lần sau khi component mounted, ko gọi khi re-render
15. useEffect(callback, [deps])
  - gọi callback mỗi khi deps thay đổi
16. callback luôn được gọi sau khi component mounted(đúng cho cả 3 TH)
17. sideEffects
  - dùng useEffect là dùng sideEffect, là các hiệu ứng bên lề, ta ưu tiên render ra element hay dao diện người dùng trước, rồi mới thực hiện
side effect, useEffect giúp element render ra trước rồi mới thực hiện callback hay thực hiện sideEffect. Nếu không dùng useEffect, các câu lệnh
thông thường có thể thực thi trước khi giao diện render xong -> gây xung đột 
18. khi dùng eventlistener phạm vi window trong 1 component, khi component đó bị unmounted thì eventlistener không bị xóa mà vẫn tồn tại trong bộ nhớ,
component mounted lại sẽ tạo ra 1 eventlistener mới với phạm vi khác trong khi event cũ vẫn trong bộ nhớ mà không thể dùng lại -> cần remove event khi
component unmounted -> dùng cleanup function
19. cleanup function luôn được gọi trước khi component unmounted (đúng cả 3 TH)
  VD: return () => {
    window.removeEvenlistener(...)
    hoặc 
    clearInterval(...)
  }
20. cleanup function luôn được gọi trước khi callback được gọi (trừ lần mounted)
  VD: khi deps thay đổi, cleanup thực hiện với trạng thái cũ trước khi chạy callbacck của trạng thái mới
21. useEffect & useLayoutEffect
  * useEffect
  1. cập nhật lại state
  2. cập nhật DOM (mutated)
  3. render lại UI
  4. gọi cleanup nếu deps thay đổi 
  5. gọi useEffect callback 
  * useLayoutEffect
  1. cập nhật lại state
  2. cập nhật DOM (mutated)
  3. gọi cleanup nếu deps thay đổi (sync)
  4. gọi useLayoutEffect callback (sync)
  5. render lại UI
22. useRef: giữ tham chiếu đến một DOM element hoặc giá trị bất kỳ mà không bị reset sau mỗi lần render lại component
  - việc khai báo let một biến trong hàm App thì mỗi lần gọi lại hàm App bằng useState thì 1 scope mới được tạo ra, biến trong scope cũ
không còn được sử dụng. VD scope cũ có biến ID của setInterval thì khi render lại App tạo scope mới thì ID cũ sẽ không thể dùng lại để
clearInterval. Có thể khai báo biến ở bên ngoài hàm App, tuy nhiên sẽ vi phạm quy ước trình bày code -> dùng useRef
  - useRef giúp khắc phục vấn đề khởi tạo lại biến mỗi lần re-render component bằng cách useRef chỉ dùng giá trị khởi tạo sau khi component mounted,
giữ lại tham chiếu đến giá trị cũ qua các lần re-render
  VD: const timerID = useRef() -> timerID sẽ chỉ được khởi tạo khi component vừa mounted và giữ lại qua các lần re-render
  - useRef nhận mọi giá trị và luôn trả về object với prop là current
23. memo() --> HOC
  - 3 khái niệm hay dùng trong React để kế thừa logic tránh lặp code
  + Hooks
  + HOC (Higher Order Component) 
  + Render props
  - memo giúp ghi nhớ lại props của 1 component để quyết định có render lại component hay không, prop thay đổi (qua state) thì render lại, không thì thôi
  - memo sẽ gặp vấn đề nếu props là một hàm được truyền vào, các hàm trong có vẻ không thay đổi nhưng khi state thay đổi, nó tạo ra một hàm mới với 
reference mới, memo so sánh giá trị ref cũ và ref mới của hàm thấy khác nhau -> component vẫn re-render 
  -> dùng useCallback để khắc phục
24. useCallback(callback, deps)
  - lưu tham chiếu callback bên ngoài App và return lại tham chiếu cho biến, nếu deps không đổi thì return lại tham chiếu cũ, deps đổi thì return tham chiếu mới
  - dùng react.memo thì các function truyền vào phải dùng useCallback, không dùng react.memo thì không dùng useCallback 
25. useMemo(callback, deps)
  - giúp không thực hiện lại một logic không cần thiết
26. useReducer
  - có thể dùng thay thế state phức tạp, lồng nhau
  - 4 bước reducer: 1. declare init state: 0
                    2. declare actions: Up (state + 1)/ Down (state - 1)
                    3. reducer
                    4. dispatch
27. Context/ createContext & useContext
  - giúp truyền dữ liệu từ component cha xuống con mà không cần dùng prop, không cần qua component chung gian
  Step: 1. create context
        2. provider
        3. consumer
  - createContext gồm 2 component provider, consumer, mỗi createContext là 1 phạm vi khác nhau
  VD: const ThemeContext = createContext()
  - dùng component provider bao toàn bộ cha, truyền vào prop
  VD: <ThemeContext.Provider value{theme}> 
      </ThemeContext.Provider>
  - dùng consumer cho con để nhận, muốn nhận phải dùng đúng biến ThemeContext (cần import nếu ở file khác nhau) -> cần dùng useContext
  VD: const theme = useContext(ThemeContext)
  - biến theme lúc này nhận value của provider 
28. Nếu không ghi rõ tên file, mặc định import sẽ chỉ đến file index
29. forwardRef (HOC)
  - giúp chuyển tiếp ref
30. useImperativeHandle()
  - dùng khi bạn muốn expose (cung cấp) một số hàm hoặc thuộc tính nhất định ra bên ngoài component con, 
thay vì để ref truy cập toàn bộ DOM hoặc toàn bộ instance.
  - useImperativeHandle(ref, () => ({
      // exposed methods or properties
    }), [dependencies]);
  - ref: là ref được truyền từ component cha vào qua forwardRef.

    Callback return ra một object chứa các method/property mà bạn muốn expose ra.

    Mảng dependencies để xác định khi nào cần cập nhật lại.
31. CSS khi chạy chế độ dev là CSS internal, chế độ Production là CSS external
32. CSS module
  - Khi dùng và import CSS module, VD: import styles from './Paragraph.module.css' thì react sẽ đưa các class thành props của objects
styles và value của các props chính là tên class mới được mã hóa khác nhau theo đường dẫn
  - Ưu: không bị trùng css, css của mỗi component hoạt động độc lập
  - Nhược: không có tính kế thừa, không nên dùng tag name làm class vì tag name không module được
  - Đặt tên class theo camelCase
  - Giải quyết việc không có tính kế thừa bằng cách tạo riêng một thư mục với component GlobalStyles và file css của nó, rồi dùng component đó
bao toàn bộ code ở return trong App
  VD: function GlobalStyles({children}) {
    return children
  }
33. clsx
  - clsx giúp đưa class vào prop một cách gọn gàng hơn
  VD: className = {clsx(styles.btn, styles.active)}
  thay vì: className = {`${styles.btn} ${styles.active}`}
  - khi truyền object và clsx thì clsx sẽ: 
  1. Nhận object.
  2. Duyệt từng key:
    Nếu value là true, giữ lại key đó.
    Nếu false, bỏ qua.
  3. Ghép các key hợp lệ thành chuỗi cách nhau bằng dấu cách, và chú ý chính tên key sẽ là tên class
  - có thể kết hợp với GlobalStyles bằng cách đơn giản là thêm tên class vào clsx dưới dạng chuỗi
  VD: trong GlobalStyles có class .flex
  thì có thể viết className = {clsx(styles.btn, 'flex', styles.active)}
34. import.meta 
  - là một object đặc biệt trong các module JavaScript (ES Module – import/export). Nó cung cấp thông tin về chính file module đang chạy
35.
  - Link: dùng như thẻ <a>, để người dùng click → điều hướng.
  - NavLink: dùng như Link nhưng có thêm khả năng xác định "link hiện tại" bằng class active.
  - Navigate: dùng để redirect bằng logic JavaScript, không phải click.
  - useNavigate ?



acess toke & refresh token
axios/interceptors