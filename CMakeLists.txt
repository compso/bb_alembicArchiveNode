##-*****************************************************************************
##
## Copyright (c) 2009-2011,
##  Sony Pictures Imageworks Inc. and
##  Industrial Light & Magic, a division of Lucasfilm Entertainment Company Ltd.
##
## All rights reserved.
##
## Redistribution and use in source and binary forms, with or without
## modification, are permitted provided that the following conditions are
## met:
## *       Redistributions of source code must retain the above copyright
## notice, this list of conditions and the following disclaimer.
## *       Redistributions in binary form must reproduce the above
## copyright notice, this list of conditions and the following disclaimer
## in the documentation and/or other materials provided with the
## distribution.
## *       Neither the name of Sony Pictures Imageworks, nor
## Industrial Light & Magic, nor the names of their contributors may be used
## to endorse or promote products derived from this software without specific
## prior written permission.
##
## THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
## "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
## LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
## A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
## OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
## SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
## LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
## DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
## THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
## (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
## OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
##
##-*****************************************************************************

PROJECT( ALEMBIC_ARCHIVE_NODE_MAYA_MODULE )

SET( H_FILES
	bb_alembicArchiveShape.h
	Foundation.h
	IPolyMeshDrw.h
	IXformDrw.h
    ISubDDrw.h
    PathUtil.h
    timer.h
    Drawable.h
	Scene.h
	Transport.h
	DrawContext.h
	IObjectDrw.h
	MeshDrwHelper.h
	SceneManager.h
	CameraHelper.h
	CreateSceneHelper.h
	LocatorHelper.h
	MeshHelper.h
	NodeIteratorVisitorHelper.h
	NurbsCurveHelper.h
	NurbsSurfaceHelper.h
	PointHelper.h
	util.h
	XformHelper.h
)

SET( CXX_FILES
	bb_alembicArchiveShape.cpp
	IObjectDrw.cpp
	IPolyMeshDrw.cpp
	ISubDDrw.cpp
	IXformDrw.cpp
	MeshDrwHelper.cpp
	PathUtil.cpp
	pluginMain.cpp
	Scene.cpp
	Transport.cpp
	BB_AlembicArchiveTranslator.cpp
	CameraHelper.cpp
	CreateSceneHelper.cpp
	LocatorHelper.cpp
	MeshHelper.cpp
	NurbsCurveHelper.cpp
	NurbsSurfaceHelper.cpp
	NodeIteratorVisitorHelper.cpp
	PointHelper.cpp
	util.cpp
	XformHelper.cpp
)

SET( SOURCE_FILES ${CXX_FILES} ${H_FILES} )

SET( CORE_LIBS
  AlembicAbcGeom
  AlembicAbc
  AlembicAbcCoreFactory
  AlembicAbcCoreOgawa
  AlembicAbcCoreHDF5
  AlembicAbcCoreAbstract
  AlembicUtil )

INCLUDE_DIRECTORIES( ${ALEMBIC_HDF5_INCLUDE_PATH} )
INCLUDE_DIRECTORIES( ".." )
INCLUDE_DIRECTORIES( "../lib" )
INCLUDE_DIRECTORIES( ${ALEMBIC_PRMAN_INCLUDE_PATH} )
INCLUDE_DIRECTORIES( ${ALEMBIC_ARNOLD_INCLUDE_PATH} )
INCLUDE_DIRECTORIES( ${ALEMBIC_MTOA_INCLUDE_PATH} ) 
INCLUDE_DIRECTORIES( "/development/playground/maya/include" )

ADD_MAYA_CXX_PLUGIN( bb_alembicArchiveShape ${SOURCE_FILES} )
TARGET_LINK_LIBRARIES( bb_alembicArchiveShape
  ${MAYA_LIBRARIES}
  ${CORE_LIBS}
  ${ALEMBIC_HDF5_LIBS}
  ${ALEMBIC_PRMAN_LIBPRMAN}
  ${ALEMBIC_GL_LIBS}
  ${ALEMBIC_ILMBASE_LIBS}
  ${ALEMBIC_MTOA_LIBMTOA}
  ${ALEMBIC_ARNOLD_LIBARNOLD}
  ${Boost_PROGRAM_OPTIONS_LIBRARY}
  ${CMAKE_THREAD_LIBS_INIT}
  ${ZLIB_LIBRARIES} ${EXTERNAL_MATH_LIBS} )

INSTALL( TARGETS bb_alembicArchiveShape
         DESTINATION maya/$ENV{MAYA_VERSION}/plug-ins )



