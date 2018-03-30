# Numpywitharray

Recently I crossed by learning the difference between Numpy array and list in python.

I didn't know the difference between them before. Here is a good resource:

https://stackoverflow.com/questions/568962/how-do-i-create-an-empty-array-matrix-in-numpy

"You have the wrong mental model for using NumPy efficiently. NumPy arrays are stored in contiguous blocks of memory. If you want to add rows or columns to an existing array, the entire array needs to be copied to a new block of memory, creating gaps for the new elements to be stored. This is very inefficient if done repeatedly to build an array.

In the case of adding rows, your best bet is to create an array that is as big as your data set will eventually be, and then add data to it row-by-row:"


    >>> import numpy
    >>> a = numpy.zeros(shape=(5,2))
    >>> a
    array([[ 0.,  0.],
      [ 0.,  0.],
      [ 0.,  0.],
      [ 0.,  0.],
      [ 0.,  0.]])
    >>> a[0] = [1,2]
    >>> a[1] = [2,3]
    >>> a
    array([[ 1.,  2.],
      [ 2.,  3.],
      [ 0.,  0.],
      [ 0.,  0.],
      [ 0.,  0.]])
      
      
 
A NumPy array is a very different data structure from a list and is designed to be used in different ways. Your use of hstack is potentially very inefficient... every time you call it, all the data in the existing array is copied into a new one. (The append function will have the same issue.) If you want to build up your matrix one column at a time, you might be best off to keep it in a list until it is finished, and only then convert it into an array.

e.g.


    mylist = []
    for item in data:
        mylist.append(item)
    mat = numpy.array(mylist)
    
    
item can be a list, an array or any iterable, as long as each item has the same number of elements.
In this particular case (data is some iterable holding the matrix columns) you can simply use


    mat = numpy.array(data)
(Also note that using list as a variable name is probably not good practice since it masks the built-in type by that name, which can lead to bugs.)

EDIT:

If for some reason you really do want to create an empty array, you can just use  numpy.array([]), but this is rarely useful!
