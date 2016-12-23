# Unit Testing and Mocking

### Stubs vs. Mocks


### Mocking Using Categories


```
import com.agiledeveloper.CodeWithHeavierDependencies


```

### Mocking Using ExpandoMetaClass

```

class TestUsingExpandoMetaClass extends GroovyTestCase {


void testMyMethod() {
	emc.println = { text -> result = text }
	testObj.metaClass = emc
