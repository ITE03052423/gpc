# GPC: A library for the solution of General Point Correspondence problems.
# Copyright (C) 2006 Andrea Censi (andrea at censi dot org)

# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.


cmake_minimum_required(VERSION 2.6)

PROJECT (gpc C)

	INCLUDE (FindGSL.cmake) 

	IF(GSL_FOUND)
		MESSAGE(STATUS "Found GSL:")
		MESSAGE(STATUS "   GSL_LIBRARIES = ${GSL_LIBRARIES}")
		MESSAGE(STATUS "   GSL_INCLUDE_DIR = ${GSL_INCLUDE_DIR}")
		MESSAGE(STATUS "   CMAKE_GSL_CXX_FLAGS = ${CMAKE_GSL_CXX_FLAGS}")
		MESSAGE(STATUS "   GSL_LINK_DIRECTORIES = ${GSL_LINK_DIRECTORIES}")
		
		INCLUDE_DIRECTORIES(${GSL_INCLUDE_DIR})	
		LINK_DIRECTORIES(${GSL_LINK_DIRECTORIES})		 
	ELSE(GSL_FOUND)
		MESSAGE(ERROR "GSL not found.")
	ENDIF(GSL_FOUND)

SET(CMAKE_C_FLAGS "-ggdb -Wall -std=c99 -pedantic")

ADD_LIBRARY(gpc STATIC gpc.c gpc_utils.c)
TARGET_LINK_LIBRARIES(gpc ${GSL_LIBRARIES})

ADD_EXECUTABLE(gpc_test gpc_test.c)
TARGET_LINK_LIBRARIES(gpc_test gpc ${GSL_LIBRARIES})

INSTALL(TARGETS gpc ARCHIVE DESTINATION lib)
INSTALL(FILES gpc.h DESTINATION include)
INSTALL(FILES gpc_utils.h DESTINATION include)

