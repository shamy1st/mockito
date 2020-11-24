# Mockito

### Example

        //@RunWith(MockitoJUnitRunner.class)//JUnit4
        @ExtendWith(MockitoExtension.class) //JUnit5
        class BusinessTest {

            @InjectMocks
            private Business business;
            @Mock
            private DataService data;

            void test(int[] array, int expected) {
                when(data.getArray()).thenReturn(array);
                assertEquals(expected, business.sum());
            }

            @Test
            void sum_null() {
                test(null, 0);
            }

            @Test
            void sum_empty() {
                test(new int[] {}, 0);
            }

            @Test
            void sum_basic() {
                test(new int[] {7, 11, -3, 5}, 20);
            }
        }

        public interface DataService {
            int[] getArray();
        }

        public class Business {

            private DataService data;

            public void setData(DataService data) {
                this.data = data;
            }

            public int sum() {
                int[] array = data.getArray();
                if(array == null)
                    return 0;

                int sum = 0;
                for(int value : array) {
                    sum += value;
                }
                return sum;
            }
        }


