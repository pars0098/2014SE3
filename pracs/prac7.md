White-box Testing 2048

In these test each code path will be tested and the bounds of each condition tested.

The first code path to be tested is creating the board. The minimum board size is 1, and the maximum is 255. If the size is outside the bounds the board is not created and 0 is returned. Tests to create the board of size 1 and 255 should both return a board, while 0 and 256 should return NULL.

A new function is added to test.c

int board_create_test(int size) {
	int **board = board_create(size);
	if (board==0&&(size>0&&size<256)) {
		printf("FAILED - Creating board size %d\n", size);
		return -1;
	}
	else {
		printf("PASSED\n");
		return 0;
	}
}

And called with the following values

  e|=board_create_test(1);
  e|=board_create_test(255);
  e|=board_create_test(0);
  e|=board_create_test(256);

The tests are run and the output is the following

PASSED
PASSED
PASSED
PASSED

The next test is to ensure that the board created is accessable, and that values can be written to and read from each square in the board. This test will only be run on board sizes 1 and 255.

int board_access_test(int size) {
	int **board = board_create(size);
	if (board==0&&(size>0&&size<256)) {
		printf("FAILED - Creating board size %d\n", size);
		return -1;
	}
	else {
		if (board!=0) {
			int i = 0;
			while (i < size) {
				int j = 0;
				while (j < size) {
						int t = 10000000; //a very large number
						board[i][j] = t;
						
						if (board[i][j]!=t) {
							printf("FAILED - Accessing board size %d\n at %d,%d", size,i,j);
							return -1;
						}
					j++
				}
				i++;
			}
		}
		printf("PASSED\n");
		return 0;
	}
}

This test is called after the board create tests, with the following values

  e|=board_access_test(1);
  e|=board_access_test(255);



The next code path to test is sliding the board in a particular direction.  This test will require a function to create a board of a certain size, and fill the board with values - a known state - then execute a function on the board and validate the results. The function header is shown below - the mechanics are in the source code.

int board4_vector_test(int i1,int i2,int i3,int i4,
					   int i5,int i6,int i7,int i8,
					   int i9,int i10,int i11,int i12,
					   int i13,int i14,int i15,int i16,
					   char *msg,
                       int o1,int o2,int o3,int o4,
					   int o5,int o6,int o7,int o8,
					   int o9,int o10,int o11,int o12,
					   int o13,int o14,int o15,int o16,
                       int (*func)(int,int **)
					   ) { ... }
