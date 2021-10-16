CMAKE_MINIMUM_REQUIRED  (VERSION 3.12)
PROJECT                 (Iconv)

# options
OPTION                  (ICONV_BUILD_SHARED_LIBS "Build shared libraries" ON)
OPTION                  (ICONV_BUILD_STATIC_LIBS "Build static libraries" ON)

# needed packages
SET                     (CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake_modules")

# includes and outputs
SET                     (CMAKE_INCLUDE_CURRENT_DIR on)
SET                     (INCLUDE_DIR "${PROJECT_SOURCE_DIR}/include")
INCLUDE_DIRECTORIES     (BEFORE SYSTEM
                          ${INCLUDE_DIR}
                          "${PROJECT_SOURCE_DIR}/libcharset/include"
                          "${PROJECT_SOURCE_DIR}/include"
                          "${PROJECT_SOURCE_DIR}/"
                          "${PROJECT_SOURCE_DIR}/win32"
                          "${PROJECT_SOURCE_DIR}/win32/private"
                        )

# compiler settings
SET                     (CMAKE_CXX_STANDARD 17)
SET                     (CMAKE_CXX_STANDARD_REQUIRED on)
# Linux
IF                      (${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
#  MESSAGE                 ("Unix-like system: ${CMAKE_SYSTEM_NAME}")
# Windows
ELSEIF                  (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
  MESSAGE                 ("Windows-like system: ${CMAKE_SYSTEM_NAME}")
# Unsupported
ELSE                    ()
  MESSAGE                 (FATAL_ERROR "unsupported system: ${CMAKE_SYSTEM_NAME}")
ENDIF                   ()

# source code stuff starts here

SET                     (tmpFiles 
                          #${PROJECT_SOURCE_DIR}/lib/aliases.gperf
                          #${PROJECT_SOURCE_DIR}/lib/aliases_sysaix.gperf
                          #${PROJECT_SOURCE_DIR}/lib/aliases_syshpux.gperf
                          #${PROJECT_SOURCE_DIR}/lib/aliases_sysosf1.gperf
                          #${PROJECT_SOURCE_DIR}/lib/aliases_syssolaris.gperf
                          #${PROJECT_SOURCE_DIR}/lib/encodings.def
                          #${PROJECT_SOURCE_DIR}/lib/encodings_aix.def
                          #${PROJECT_SOURCE_DIR}/lib/encodings_dos.def
                          #${PROJECT_SOURCE_DIR}/lib/encodings_extra.def
                          #${PROJECT_SOURCE_DIR}/lib/encodings_local.def
                          #${PROJECT_SOURCE_DIR}/lib/encodings_osf1.def
                          #${PROJECT_SOURCE_DIR}/lib/translit.def
                          ${PROJECT_SOURCE_DIR}/lib/iconv.c
                          ${PROJECT_SOURCE_DIR}/lib/relocatable.c

                          ${PROJECT_SOURCE_DIR}/libcharset/lib/localcharset.c
                          ${PROJECT_SOURCE_DIR}/libcharset/lib/relocatable-stub.c

                          ${PROJECT_SOURCE_DIR}/libcharset/include/libcharset.h
                          ${PROJECT_SOURCE_DIR}/libcharset/include/localcharset.h

                          ${PROJECT_SOURCE_DIR}/include/iconv.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases.h
                          ${PROJECT_SOURCE_DIR}/lib/aliases2.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_aix.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_aix_sysaix.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_dos.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_extra.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_osf1.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_osf1_sysosf1.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_sysaix.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_syshpux.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_sysosf1.h
                          #${PROJECT_SOURCE_DIR}/lib/aliases_syssolaris.h
                          ${PROJECT_SOURCE_DIR}/lib/armscii_8.h
                          ${PROJECT_SOURCE_DIR}/lib/ascii.h
                          ${PROJECT_SOURCE_DIR}/lib/atarist.h
                          ${PROJECT_SOURCE_DIR}/lib/big5.h
                          ${PROJECT_SOURCE_DIR}/lib/big5hkscs1999.h
                          ${PROJECT_SOURCE_DIR}/lib/big5hkscs2001.h
                          ${PROJECT_SOURCE_DIR}/lib/big5hkscs2004.h
                          ${PROJECT_SOURCE_DIR}/lib/big5hkscs2008.h
                          ${PROJECT_SOURCE_DIR}/lib/big5_2003.h
                          ${PROJECT_SOURCE_DIR}/lib/c99.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_aix.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_aix_sysaix.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_dos.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_extra.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_local.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_local_sysaix.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_local_syshpux.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_local_sysosf1.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_local_syssolaris.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_osf1.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_osf1_sysosf1.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_sysaix.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_syshpux.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_sysosf1.h
                          #${PROJECT_SOURCE_DIR}/lib/canonical_syssolaris.h
                          ${PROJECT_SOURCE_DIR}/lib/ces_big5.h
                          ${PROJECT_SOURCE_DIR}/lib/ces_gbk.h
                          ${PROJECT_SOURCE_DIR}/lib/cjk_variants.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_1.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_15.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_2.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_3.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_4.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_4a.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_4b.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_5.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_6.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_7.h
                          ${PROJECT_SOURCE_DIR}/lib/cns11643_inv.h
                          ${PROJECT_SOURCE_DIR}/lib/config.h
                          ${PROJECT_SOURCE_DIR}/lib/converters.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1046.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1124.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1125.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1129.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1131.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1133.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1161.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1162.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1163.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1250.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1251.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1252.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1253.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1254.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1255.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1256.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1257.h
                          ${PROJECT_SOURCE_DIR}/lib/cp1258.h
                          ${PROJECT_SOURCE_DIR}/lib/cp437.h
                          ${PROJECT_SOURCE_DIR}/lib/cp50221_0208_ext.h
                          ${PROJECT_SOURCE_DIR}/lib/cp50221_0212_ext.h
                          ${PROJECT_SOURCE_DIR}/lib/cp737.h
                          ${PROJECT_SOURCE_DIR}/lib/cp775.h
                          ${PROJECT_SOURCE_DIR}/lib/cp850.h
                          ${PROJECT_SOURCE_DIR}/lib/cp852.h
                          ${PROJECT_SOURCE_DIR}/lib/cp853.h
                          ${PROJECT_SOURCE_DIR}/lib/cp855.h
                          ${PROJECT_SOURCE_DIR}/lib/cp856.h
                          ${PROJECT_SOURCE_DIR}/lib/cp857.h
                          ${PROJECT_SOURCE_DIR}/lib/cp858.h
                          ${PROJECT_SOURCE_DIR}/lib/cp860.h
                          ${PROJECT_SOURCE_DIR}/lib/cp861.h
                          ${PROJECT_SOURCE_DIR}/lib/cp862.h
                          ${PROJECT_SOURCE_DIR}/lib/cp863.h
                          ${PROJECT_SOURCE_DIR}/lib/cp864.h
                          ${PROJECT_SOURCE_DIR}/lib/cp865.h
                          ${PROJECT_SOURCE_DIR}/lib/cp866.h
                          ${PROJECT_SOURCE_DIR}/lib/cp869.h
                          ${PROJECT_SOURCE_DIR}/lib/cp874.h
                          ${PROJECT_SOURCE_DIR}/lib/cp922.h
                          ${PROJECT_SOURCE_DIR}/lib/cp932.h
                          ${PROJECT_SOURCE_DIR}/lib/cp932ext.h
                          ${PROJECT_SOURCE_DIR}/lib/cp936.h
                          ${PROJECT_SOURCE_DIR}/lib/cp936ext.h
                          ${PROJECT_SOURCE_DIR}/lib/cp943.h
                          ${PROJECT_SOURCE_DIR}/lib/cp949.h
                          ${PROJECT_SOURCE_DIR}/lib/cp950.h
                          ${PROJECT_SOURCE_DIR}/lib/cp950ext.h
                          ${PROJECT_SOURCE_DIR}/lib/dec_hanyu.h
                          ${PROJECT_SOURCE_DIR}/lib/dec_kanji.h
                          ${PROJECT_SOURCE_DIR}/lib/euc_cn.h
                          ${PROJECT_SOURCE_DIR}/lib/euc_jisx0213.h
                          ${PROJECT_SOURCE_DIR}/lib/euc_jp.h
                          ${PROJECT_SOURCE_DIR}/lib/euc_kr.h
                          ${PROJECT_SOURCE_DIR}/lib/euc_tw.h
                          #${PROJECT_SOURCE_DIR}/lib/flags.h
                          ${PROJECT_SOURCE_DIR}/lib/flushwc.h
                          ${PROJECT_SOURCE_DIR}/lib/gb12345.h
                          ${PROJECT_SOURCE_DIR}/lib/gb12345ext.h
                          ${PROJECT_SOURCE_DIR}/lib/gb18030.h
                          ${PROJECT_SOURCE_DIR}/lib/gb18030ext.h
                          ${PROJECT_SOURCE_DIR}/lib/gb18030uni.h
                          ${PROJECT_SOURCE_DIR}/lib/gb2312.h
                          ${PROJECT_SOURCE_DIR}/lib/gbk.h
                          ${PROJECT_SOURCE_DIR}/lib/gbkext1.h
                          ${PROJECT_SOURCE_DIR}/lib/gbkext2.h
                          ${PROJECT_SOURCE_DIR}/lib/gbkext_inv.h
                          ${PROJECT_SOURCE_DIR}/lib/georgian_academy.h
                          ${PROJECT_SOURCE_DIR}/lib/georgian_ps.h
                          ${PROJECT_SOURCE_DIR}/lib/hkscs1999.h
                          ${PROJECT_SOURCE_DIR}/lib/hkscs2001.h
                          ${PROJECT_SOURCE_DIR}/lib/hkscs2004.h
                          ${PROJECT_SOURCE_DIR}/lib/hkscs2008.h
                          ${PROJECT_SOURCE_DIR}/lib/hp_roman8.h
                          ${PROJECT_SOURCE_DIR}/lib/hz.h
                          ${PROJECT_SOURCE_DIR}/lib/iconv_open1.h
                          ${PROJECT_SOURCE_DIR}/lib/iconv_open2.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_cn.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_cnext.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_jp.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_jp1.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_jp2.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_jp3.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_jpms.h
                          ${PROJECT_SOURCE_DIR}/lib/iso2022_kr.h
                          ${PROJECT_SOURCE_DIR}/lib/iso646_cn.h
                          ${PROJECT_SOURCE_DIR}/lib/iso646_jp.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_1.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_10.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_11.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_13.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_14.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_15.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_16.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_2.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_3.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_4.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_5.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_6.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_7.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_8.h
                          ${PROJECT_SOURCE_DIR}/lib/iso8859_9.h
                          ${PROJECT_SOURCE_DIR}/lib/isoir165.h
                          ${PROJECT_SOURCE_DIR}/lib/isoir165ext.h
                          ${PROJECT_SOURCE_DIR}/lib/java.h
                          ${PROJECT_SOURCE_DIR}/lib/jisx0201.h
                          ${PROJECT_SOURCE_DIR}/lib/jisx0208.h
                          ${PROJECT_SOURCE_DIR}/lib/jisx0212.h
                          ${PROJECT_SOURCE_DIR}/lib/jisx0213.h
                          ${PROJECT_SOURCE_DIR}/lib/johab.h
                          ${PROJECT_SOURCE_DIR}/lib/johab_hangul.h
                          ${PROJECT_SOURCE_DIR}/lib/koi8_r.h
                          ${PROJECT_SOURCE_DIR}/lib/koi8_ru.h
                          ${PROJECT_SOURCE_DIR}/lib/koi8_t.h
                          ${PROJECT_SOURCE_DIR}/lib/koi8_u.h
                          ${PROJECT_SOURCE_DIR}/lib/ksc5601.h
                          ${PROJECT_SOURCE_DIR}/lib/loops.h
                          ${PROJECT_SOURCE_DIR}/lib/loop_unicode.h
                          ${PROJECT_SOURCE_DIR}/lib/loop_wchar.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_arabic.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_centraleurope.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_croatian.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_cyrillic.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_greek.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_hebrew.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_iceland.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_roman.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_romania.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_thai.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_turkish.h
                          ${PROJECT_SOURCE_DIR}/lib/mac_ukraine.h
                          ${PROJECT_SOURCE_DIR}/lib/mulelao.h
                          ${PROJECT_SOURCE_DIR}/lib/nextstep.h
                          ${PROJECT_SOURCE_DIR}/lib/pt154.h
                          ${PROJECT_SOURCE_DIR}/lib/relocatable.h
                          ${PROJECT_SOURCE_DIR}/lib/riscos1.h
                          ${PROJECT_SOURCE_DIR}/lib/rk1048.h
                          ${PROJECT_SOURCE_DIR}/lib/shift_jisx0213.h
                          ${PROJECT_SOURCE_DIR}/lib/sjis.h
                          ${PROJECT_SOURCE_DIR}/lib/tcvn.h
                          ${PROJECT_SOURCE_DIR}/lib/tds565.h
                          ${PROJECT_SOURCE_DIR}/lib/tis620.h
                          #${PROJECT_SOURCE_DIR}/lib/translit.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs2.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs2be.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs2internal.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs2le.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs2swapped.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs4.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs4be.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs4internal.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs4le.h
                          ${PROJECT_SOURCE_DIR}/lib/ucs4swapped.h
                          ${PROJECT_SOURCE_DIR}/lib/uhc_1.h
                          ${PROJECT_SOURCE_DIR}/lib/uhc_2.h
                          ${PROJECT_SOURCE_DIR}/lib/utf16.h
                          ${PROJECT_SOURCE_DIR}/lib/utf16be.h
                          ${PROJECT_SOURCE_DIR}/lib/utf16le.h
                          ${PROJECT_SOURCE_DIR}/lib/utf32.h
                          ${PROJECT_SOURCE_DIR}/lib/utf32be.h
                          ${PROJECT_SOURCE_DIR}/lib/utf32le.h
                          ${PROJECT_SOURCE_DIR}/lib/utf7.h
                          ${PROJECT_SOURCE_DIR}/lib/utf8.h
                          ${PROJECT_SOURCE_DIR}/lib/vietcomb.h
                          ${PROJECT_SOURCE_DIR}/lib/viscii.h

                          ${PROJECT_SOURCE_DIR}/include/iconv.h
                          ${PROJECT_SOURCE_DIR}/res/libiconv.rc

                          #${PROJECT_SOURCE_DIR}/LICENSE
                          #${PROJECT_SOURCE_DIR}/README.md
                        )
SOURCE_GROUP            (TREE ${PROJECT_SOURCE_DIR} FILES ${tmpFiles})

SET                     (TPL_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG}")
SET                     (TPL_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE}")

IF                      (CMAKE_CONFIGURATION_TYPES)
  SET                     (CMAKE_CONFIGURATION_TYPES Debug Release)
  SET                     (CMAKE_CONFIGURATION_TYPES "${CMAKE_CONFIGURATION_TYPES}" CACHE STRING "Reset the configurations to what we need" FORCE)
ENDIF                   ()

IF                      (ICONV_BUILD_STATIC_LIBS)
  SET                     (CMAKE_CXX_FLAGS_DEBUG "${TPL_FLAGS_DEBUG} -D_LIB -DUSING_STATIC_LIBICONV")
  SET                     (CMAKE_CXX_FLAGS_RELEASE "${TPL_FLAGS_RELEASE} -D_LIB -DUSING_STATIC_LIBICONV")

  ADD_LIBRARY             (iconvStatic STATIC ${tmpFiles})
  SET_TARGET_PROPERTIES	  (iconvStatic PROPERTIES LINKER_LANGUAGE CXX)
ENDIF                   ()
IF                      (ICONV_BUILD_SHARED_LIBS)
  SET                     (CMAKE_CXX_FLAGS_DEBUG "${TPL_FLAGS_DEBUG} -D_USRDLL -DBUILDING_LIBICONV -DBUILDING_LIBCHARSET -DLIBICONV_EXPORTS")
  SET                     (CMAKE_CXX_FLAGS_RELEASE "${TPL_FLAGS_RELEASE} -D_USRDLL -DBUILDING_LIBICONV -DBUILDING_LIBCHARSET -DLIBICONV_EXPORTS")

  ADD_LIBRARY             (iconv MODULE ${tmpFiles})
  SET_TARGET_PROPERTIES   (iconv PROPERTIES LINKER_LANGUAGE CXX)
ENDIF                   ()
