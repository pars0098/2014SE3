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


