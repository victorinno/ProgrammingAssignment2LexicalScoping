ProgrammingAssignment2LexicalScoping
====================================
### Introduction

This is my code for the second programming assignment.

### Code
Looks for the MASS package, if it don´t find install it
	if(!require("MASS")){
		install.packages("MASS")
	}
Calls the MASS package
	library("MASS")

This function creates a structure that receives any matrix and can keep it cached
it also possible to keep the inverse of the matrix cached
	makeCacheMatrix  <- function(matrix = matrix()){
		invMatrix <- NULL
		
		setMatrix <- function(sMatrix){
			matrix <<- sMatrix
			invMatrix <<- NULL
		}
		
		getMatrix <- function(){
			matrix
		}
		
		setInvMatrix <- function(sInvMatrix){
			invMatrix <<- sInvMatrix
		}
		
		getInvMatrix <- function(){
			invMatrix
		}
		list(setMatrix = setMatrix,
			 getMatrix = getMatrix,
			 setInvMatrix = setInvMatrix,
			 getInvMatrix = getInvMatrix)
}

This function looks for a cached inversed matrix, if it finds the function 
returns the cached value, if it don´t find the function reverse
the value passed as a parameter, caches it and return the reverted matrix value
	cacheSolve  <- function(makeCacheMatrix , ...){
		inv <- makeCacheMatrix $getInvMatrix()
		
		if(!is.null(inv)){
			message("Getting cached inverted matrix")
			return(inv)
		}
		
		data <- makeCacheMatrix $getMatrix()
		
		inv <- ginv(data)
		
		makeCacheMatrix $setInvMatrix(inv)
		
		inv
	}