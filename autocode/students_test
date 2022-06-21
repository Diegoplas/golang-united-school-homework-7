package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeople_Len(t *testing.T) {

	bday1 := time.Date(1996, 22, 02, 20, 34, 58, 651387237, time.UTC)
	bday2 := time.Date(1998, 04, 05, 20, 34, 58, 651387237, time.UTC)
	bday3 := time.Date(1999, 12, 07, 20, 34, 58, 651387237, time.UTC)

	testPeopleLen := People{
		Person{"testName1", "testLN1", bday1},
		Person{"testName2", "testLN2", bday2},
		Person{"testName3", "testLN3", bday3},
	} 

	emptyPeopleLen := People{} 

	tests := []struct {
		name string
		p    People
		want int
	}{
		{
			name: "Valid Len Test",
			p: testPeopleLen,
			want: 3,
		},
		{
			name: "Empty Len Test",
			p: emptyPeopleLen,
			want: 0,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Len(); got != tt.want {
				t.Errorf("People.Len() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Less(t *testing.T) {

	BDay1 := time.Date(1996, 22, 02, 20, 34, 58, 651387237, time.UTC)

	AfterBDay1 := time.Date(2000, 15, 06, 20, 34, 58, 651387237, time.UTC)

	testLessLastNames := People{
		Person{"SameFirstName", "A_SmallerLastName", BDay1},
		Person{"SameFirstName", "Z_BiggerLastName", BDay1},
	} 

	testLessFirstNames := People{
		Person{"Z_BiggerFirstName", "SameLastName", BDay1},
		Person{"A_BiggerFirstName", "SameLastName", BDay1},
	} 
	
	testLessBDays := People{
		Person{"SameFirstName", "SameLastName", AfterBDay1},
		Person{"SameFirstName", "SameLastName", BDay1},
	} 
	
	
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want bool
	}{
		{
			name: "Valid Less Test - Bigger second LastName",
			p: testLessLastNames,
			args: args{0,1},
			want: true,
		},
		{
			name: "Valid Less Test - Bigger first FirstName",
			p: testLessFirstNames,
			args: args{0,1},
			want: false,
		},
		{
			name: "Valid Less Test - Bigger first BDay",
			p: testLessBDays,
			args: args{0,1},
			want: true,
		},
		
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Less(tt.args.i, tt.args.j); got != tt.want {
				t.Errorf("People.Less() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	bday1 := time.Date(1996, 22, 02, 20, 34, 58, 651387237, time.UTC)
	bday2 := time.Date(1998, 04, 05, 20, 34, 58, 651387237, time.UTC)
	bday3 := time.Date(1999, 12, 07, 20, 34, 58, 651387237, time.UTC)
	
	testPeopleSwap := People{
		Person{"testName1", "testLN1", bday1},
		Person{"testName2", "testLN2", bday2},
		Person{"testName3", "testLN3", bday3},
	}

	type args struct {
		i int
		j int
	}

	tests := []struct {
		name string
		p    People
		args args
	}{
		{
			name: "Valid Swap Test",
			p: testPeopleSwap,
			args: args{0,2},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.p.Swap(tt.args.i, tt.args.j)
		})
	}
}

/////////////////////////////////////////////////////////////

func TestNew(t *testing.T) {
	validTestString := "1 2 3 4\n 5 6 7 8"
	invalidTestString := "1 A 3 4\n 5 6 7 8"
	diffSizeColTestString := "1 2 3 4\n 5 6 7 8 9"
	type args struct {
		str string
	}
	tests := []struct {
		name    string
		args    args
		want    *Matrix
		wantErr bool
	}{
		{
			name: "Valid New Test",
			args: args{str: validTestString},
			want: &Matrix{
				rows: 2,
				cols: 4,
				data: []int{1,2,3,4,5,6,7,8},
			},
			wantErr: false,
		},
		{
			name: "Invalid New Test - not same lenght columns",
			args: args{str: diffSizeColTestString},
			want: nil,
			wantErr: true,
		},
		{
			name: "Invalid New Test - wrong character",
			args: args{str: invalidTestString},
			want: nil,
			wantErr: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := New(tt.args.str)
			if (err != nil) != tt.wantErr {
				t.Errorf("New() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("New() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Rows(t *testing.T) {
	type rowFields struct {
		rows int
		cols int
		data []int
	}

	testMatrixRows := rowFields{
		rows: 3,
		cols: 2,
		data: []int{1,2,3,4,5,6},
	}

	tests := []struct {
		name   string
		rowFields rowFields
		want   [][]int
	}{
		{
			name: "Valid Rows Test",
			rowFields: testMatrixRows,
			want: [][]int{
				{1,2},
				{3,4},
				{5,6},
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.rowFields.rows,
				cols: tt.rowFields.cols,
				data: tt.rowFields.data,
			}
			if got := m.Rows(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Matrix.Rows() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Cols(t *testing.T) {
	type colFields struct {
		rows int
		cols int
		data []int
	}
	testMatrixCols := colFields{
		rows: 3,
		cols: 2,
		data: []int{1,2,3,4,5,6},
	}
	tests := []struct {
		name   string
		colFields colFields
		want   [][]int
	}{
		{
			name: "Valid Cols Test",
			colFields: testMatrixCols,
			want: [][]int{
				{1,3,5},
				{2,4,6},
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.colFields.rows,
				cols: tt.colFields.cols,
				data: tt.colFields.data,
			}
			if got := m.Cols(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Matrix.Cols() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Set(t *testing.T) {
	type fieldsSet struct {
		rows int
		cols int
		data []int
	}
	testMatrixSet := fieldsSet{
		rows: 3,
		cols: 2,
		data: []int{1,2,3,4,5,6},
	}
	type args struct {
		row   int
		col   int
		value int
	}
	tests := []struct {
		name   string
		fieldsSet fieldsSet
		args   args
		want   bool
	}{
		{
			name: "Valid Set Test",
			fieldsSet: testMatrixSet,
			args: args{
				row: 2,
				col: 1, 
				value: 9,
			},
			want: true,
		},	
		{
			name: "Invalid Set Test - false, row bigger than expected",
			fieldsSet: testMatrixSet,
			args: args{
				row: 5,
				col: 2, 
				value: 9,
			},
			want: false,
		},	
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := &Matrix{
				rows: tt.fieldsSet.rows,
				cols: tt.fieldsSet.cols,
				data: tt.fieldsSet.data,
			}
			if got := m.Set(tt.args.row, tt.args.col, tt.args.value); got != tt.want {
				t.Errorf("Matrix.Set() = %v, want %v", got, tt.want)
			}
		})
	}
}