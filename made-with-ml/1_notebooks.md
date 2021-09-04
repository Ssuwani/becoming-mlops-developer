# Notebooks

글에 별 내용이 없지만 노트북을 사용하다가 자주 사용하는 명령어, 팁을 적어보려 한다.



**자주 사용하는 명령어**

`esc` : Change to Command Mode

`a` : Insert cell above

`b` : Insert cell below

`x`: Cut selected cell

`c` : Copy selected cell

`v` : Paste copied cell

`d*d ` : delete cell

`shift + enter` : Execute and move to below cell



**매직 커맨드**

마법같은 기능을 제공해주는 커맨드이다.

`%lsmagic` : 사용가능한 매직 커맨드를 보여준다.

`%time` : 바로 뒤에 오는 커맨드의 실행 시간을 알려준다.

`%%time` : 셀의 실행 시간을 알려준다.

`%timeit` : time + iteration으로 바로 뒤에오는 명령어를 여러번 반복 수행해서 평균 시간을 알려준다.

`%%timeit`: 셀의 명령어를 여러분 반복 수행해서 평균 시간을 알려준다.

`%%html`: 현재 셀을 내용을 HTML로 실행한다.

`%%python` : 현재 셀의 내용을 python 으로 실행한다.

`%%js`: 현재 셀의 내용을 javascript로 실행한다.



`%%js` 의 예시!! 크롬 개발자 도구 Console창을 확인해보자!

```bash
%%javascript
console.log("HI")
```



