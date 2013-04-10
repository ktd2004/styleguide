## vim:set ft=moin ts=4 sw=4 sts=4 sta ai si bs=2 et:

= google style guide 최신 가져오기 =
대략적으로 다음과 같은 순서로 가져올 수 있다.
 {{{
$ pwd
my_cppguide

$ cd ..
$ git svn clone http://google-styleguide.googlecode.com/svn/trunk/ --no-metadata temp_git
$ cd my_cppguide
$ git remote add trunk ../temp_git
$ git fetch
$ git checkout -b feature/trunk
$ git merge trunk/master
$ git checkout master
$ git remote rm trunk
$ rm -fr ../temp_git
 }}}


= xml2po를 사용해 변환하기 =
xml에서 pot 생성하기
 {{{
$ xml2po -e -o po/cppguide.pot cppguide.xml
 }}}

pot에서 po를 갱신
 {{{
$ msgmerge --update --backup=none --no-wrap --quiet --no-fuzzy-matching --sort-output cppguide_kr.po cppguide.pot
 }}}

원본 xml과 po 파일로 번역된 xml 만들기
 {{{
$ xml2po -p po/cppguide_kr.po cppguide.xml > cppguide.kr.xml

$ cp -af cppguide.kr.xml /var/www/html/cppguide/
$ cp -af cppguide.xml /var/www/html/cppguide/
$ cp -af styleguide.css /var/www/html/cppguide/
$ cp -af styleguide.xsl /var/www/html/cppguide/
 }}}


= 번역시 주의사항 =
 * 소스(CODE_SNIPPET)은 번역하지 말것. 번역하면 xml에서 제대로 보이지 않게됨.
