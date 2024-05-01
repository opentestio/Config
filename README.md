# Configuring Third-Party Tools

## checkstyle

- http://checkstyle.sourceforge.net
- https://github.com/checkstyle/checkstyle

## Google Style 기반으로 재작성 함

### SuppressionFilter
`SuppressionFilter`는 IntelliJ에 등록시 에러때문에 제거한다.

**before**
```xml
  <module name="SuppressionFilter">
    <property name="file" value="${org.checkstyle.google.suppressionfilter.config}"
           default="checkstyle-suppressions.xml" />
    <property name="optional" value="true"/>
  </module>
```

**after**
```xml
  <!--
  <module name="SuppressionFilter">
    <property name="file" value="${org.checkstyle.google.suppressionfilter.config}"
           default="checkstyle-suppressions.xml" />
    <property name="optional" value="true"/>
  </module>
  -->
```

### LineLength
`LineLength`는 120으로 조정한다. 주석의 길이는 무시하도록 하자. `^ *\* .*$`
[공홈의 자바독주석 무시하는 예제는 안되던데...](https://checkstyle.sourceforge.io/config_sizes.html#LineLength)

```xml
  <module name="LineLength">
    <property name="fileExtensions" value="java"/>
    <property name="max" value="120"/>
    <property name="ignorePattern" value="^package.*|^import.*|a href|href|http://|https://|ftp://|^ *\* .*$"/>
  </module>
```

### RegexpSingleline
`RegexpSingleline`추가한다
```xml
  <module name="RegexpSingleline">
    <property name="format" value="^(?!\s+\* $).*?\s+$"/>
  </module>
```

### AvoidStarImport
`AvoidStarImport`에서 static import는 Start Import를 허용한다
```xml
    <module name="AvoidStarImport"/>
```
```xml
    <module name="AvoidStarImport">
      <property name="allowStaticMemberImports" value="true"/>
      <!--
      <message key="import.avoidStar" value="static import 에만 ''.*''를 허용한다. - {0}."/>
      -->
    </module>
```

### VariableDeclarationUsageDistance
기본값이 3인데 너무 빡빡한거 아닌가? 이 속성은 사용하고 싶지 않다. 일단 크게 잡아 놓자.
https://checkstyle.sourceforge.io/config_coding.html#VariableDeclarationUsageDistance
**before**
```
    <module name="VariableDeclarationUsageDistance"/>
```
**after**
```
    <module name="VariableDeclarationUsageDistance">
      <property name="allowedDistance" value="30"/>
    </module>
```

### SingleLineJavadoc

**before**
```xml
  <module name="SingleLineJavadoc"/>
```

**after**
```xml
  <module name="SingleLineJavadoc">
    <property name="ignoreInlineTags" value="false"/>
  </module>
```
---
