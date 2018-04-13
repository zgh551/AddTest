C2000_HOME = r'/home/git/ti/ccsv7/tools/compiler/ti-cgt-c2000_16.9.6.LTS'
DEVICE     = 'TMS320F28335' 
ProjName   = 'AddTest'
import os 
import sys
PROJECT_ROOT = os.getcwd()

C2000_BIN = os.path.join(C2000_HOME, 'bin')
C2000_LIB = os.path.join(C2000_HOME, 'lib')
C2000_INC = os.path.join(C2000_HOME, 'include')

UNITY_INC = os.path.join(PROJECT_ROOT, 'Unity/inc')
CALCULATE_INC = os.path.join(PROJECT_ROOT, 'Module/inc')
BUILD_INC = os.path.join(PROJECT_ROOT, 'Debug')

#################################################################################################
env = Environment(
CFLAGS = '-v28 -ml -mt --float_support=fpu32 --include_path="%s" --include_path="%s" --include_path="%s" --advice:performance=all -g --printf_support=minimal --diag_warning=225 --diag_wrap=off --display_error_number --obj_directory="%s"' % (C2000_INC,UNITY_INC,CALCULATE_INC,BUILD_INC),
CC = os.path.join(C2000_BIN,'cl2000'),
CCCOM = '$CC $CFLAGS $SOURCES',
#################################################################################################
LINK = os.path.join(C2000_BIN,'cl2000'),
LINKFLAGS='-z -m"%s/%s.map" --heap_size=0x200 --stack_size=0x200 --warn_sections -i"%s" -i"%s" --reread_libs --diag_wrap=off --display_error_number --xml_link_info="%s_linkInfo.xml" --rom_model ' %(BUILD_INC,ProjName,C2000_LIB,C2000_INC,ProjName),
OUTPUTFILE = '--output_file=%s/%s.out' %(BUILD_INC,ProjName),
LIBS       = '--library=28335_RAM_lnk.cmd',
LINKCOM='$LINK $CFLAGS $LINKFLAGS $SOURCES $OUTPUTFILE $LIBS'
)
#################################################################################################
debug_dirs = os.listdir('%s' % (BUILD_INC))
for temp_file in debug_dirs:
	os.remove('%s/%s' % (BUILD_INC,temp_file))
	print('Delete the file:%s' % (temp_file))
	
dirs = os.listdir(PROJECT_ROOT)
for file in dirs:
    if os.path.isdir(file):        
		if os.path.exists('%s/src' %(file)):
			print(file)
			cof = env.Object(Glob('%s/src/*.c' % (file)))
			print(cof)
			
cof = env.Object(Glob('./*.c'))
print(cof)
#################################################################################################
print('out:=>%s' % (BUILD_INC))

cof = env.Program(Glob('%s/*.obj' % (BUILD_INC)))
print(cof)
#################################################################################################
#os.system(os.path.join(C2000_BIN,'hex2000') + ' -romwidth 16 -memwidth 16 -i -o %s.hex %s/*.out' %(ProjName,BUILD_INC))
#################################################################################################
#calculate = SConscript('Module/SConscript',exports = ['C2000_BIN','C2000_LIB','C2000_INC','ProjName','UNITY_INC','CALCULATE_INC','BUILD_INC'])
#unity     = SConscript('Unity/SConscript',exports = ['C2000_BIN','C2000_LIB','C2000_INC','ProjName','UNITY_INC','CALCULATE_INC','BUILD_INC'])
#main      = env.Object('main.c')

#pro_out   = SConscript('build/SConscript',exports = ['C2000_BIN','C2000_LIB','C2000_INC','ProjName','UNITY_INC','CALCULATE_INC','BUILD_INC'])

#pro_hex = env.Command(os.path.join(C2000_BIN,'cl2000'),'-romwidth 16 -memwidth 16 -i -o','%s.hex'(ProjName),'*.out')

