1. HandlerMapped에서 핸들러(Controller)를 찾는다.
2. HandlerAdapterMapped에서 HandlerAdapter를 찾는다.
3. HandlerAdapter에 핸들러를 전달하여 실행하고 ModelAndView를 받는다.
4. viewResolver에서 ModelAndView의 name으로 View를 찾아 Model의 값을 전달한다.

#### HandlerAdapter

1. ArgumentResolver를 사용하여 파라미터를 변환하여 핸들러를 호출한다.
2. ReturnValueHandler를 사용하여 반환값을 변환하여 ModelAndView 를 리턴한다.