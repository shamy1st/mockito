# Mockito

### Example

        class BusinessTest {

            private BusinessImpl business;

            public BusinessTest() {
                business = new BusinessImpl();
            }

            @Test
            void sum() {
                int expectedResult = 20;

                DataService dataMock = mock(DataService.class);
                when(dataMock.getArray()).thenReturn(new int[] {7, 11, -3, 5});
                business.setData(dataMock);
                int actualResult = business.sum();

                assertEquals(expectedResult, actualResult);
            }
        }

        public interface DataService {
            int[] getArray();
        }

        public class BusinessImpl {

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




