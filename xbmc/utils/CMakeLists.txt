set(SOURCES ActorProtocol.cpp
            AlarmClock.cpp
            AliasShortcutUtils.cpp
            Archive.cpp
            auto_buffer.cpp
            Base64.cpp
            BitstreamConverter.cpp
            BitstreamReader.cpp
            BitstreamStats.cpp
            BitstreamWriter.cpp
            BooleanLogic.cpp
            CharsetConverter.cpp
            CharsetDetection.cpp
            CPUInfo.cpp
            Crc32.cpp
            CryptThreading.cpp
            DatabaseUtils.cpp
            EndianSwap.cpp
            EmbeddedArt.cpp
            FileExtensionProvider.cpp
            Fanart.cpp
            FileOperationJob.cpp
            FileUtils.cpp
            fstrcmp.c
            GroupUtils.cpp
            HTMLUtil.cpp
            HttpHeader.cpp
            HttpParser.cpp
            HttpRangeUtils.cpp
            HttpResponse.cpp
            InfoLoader.cpp
            JobManager.cpp
            JSONVariantParser.cpp
            JSONVariantWriter.cpp
            LabelFormatter.cpp
            LangCodeExpander.cpp
            LegacyPathTranslation.cpp
            Locale.cpp
            log.cpp
            md5.cpp
            Mime.cpp
            Observer.cpp
            POUtils.cpp
            RecentlyAddedJob.cpp
            RegExp.cpp
            rfft.cpp
            RingBuffer.cpp
            RssManager.cpp
            RssReader.cpp
            ProgressJob.cpp
            SaveFileStateJob.cpp
            ScraperParser.cpp
            ScraperUrl.cpp
            Screenshot.cpp
            SortUtils.cpp
            Speed.cpp
            Stopwatch.cpp
            StreamDetails.cpp
            StreamUtils.cpp
            StringUtils.cpp
            StringValidation.cpp
            SysfsUtils.cpp
            SystemInfo.cpp
            Temperature.cpp
            TextSearch.cpp
            TimeUtils.cpp
            URIUtils.cpp
            UrlOptions.cpp
            Utf8Utils.cpp
            Variant.cpp
            VC1BitstreamParser.cpp
            Vector.cpp
            XBMCTinyXML.cpp
            XMLUtils.cpp)

set(HEADERS ActorProtocol.h
            AlarmClock.h
            AliasShortcutUtils.h
            Archive.h
            auto_buffer.h
            Base64.h
            BitstreamConverter.h
            BitstreamReader.h
            BitstreamStats.h
            BitstreamWriter.h
            BooleanLogic.h
            CharsetConverter.h
            CharsetDetection.h
            CPUInfo.h
            Crc32.h
            CryptThreading.h
            DatabaseUtils.h
            EndianSwap.h
            EventStream.h
            EventStreamDetail.h
            FileExtensionProvider.h
            Fanart.h
            FileOperationJob.h
            FileUtils.h
            fstrcmp.h
            Geometry.h
            GlobalsHandling.h
            GroupUtils.h
            HTMLUtil.h
            HttpHeader.h
            HttpParser.h
            HttpRangeUtils.h
            HttpResponse.h
            IArchivable.h
            ILocalizer.h
            InfoLoader.h
            IRssObserver.h
            ISerializable.h
            ISortable.h
            IXmlDeserializable.h
            Job.h
            JobManager.h
            JSONVariantParser.h
            JSONVariantWriter.h
            LabelFormatter.h
            LangCodeExpander.h
            LegacyPathTranslation.h
            Locale.h
            log.h
            MathUtils.h
            md5.h
            Mime.h
            Observer.h
            params_check_macros.h
            POUtils.h
            ProgressJob.h
            RecentlyAddedJob.h
            RegExp.h
            rfft.h
            RingBuffer.h
            RssManager.h
            RssReader.h
            SaveFileStateJob.h
            ScopeGuard.h
            ScraperParser.h
            ScraperUrl.h
            Screenshot.h
            SortUtils.h
            Speed.h
            Stopwatch.h
            StreamDetails.h
            StreamUtils.h
            StringUtils.h
            StringValidation.h
            SysfsUtils.h
            SystemInfo.h
            Temperature.h
            TextSearch.h
            TimeUtils.h
            URIUtils.h
            UrlOptions.h
            Utf8Utils.h
            Variant.h
            VC1BitstreamParser.h
            Vector.h
            XBMCTinyXML.h
            XMLUtils.h)

if(XSLT_FOUND)
  list(APPEND SOURCES XSLTUtils.cpp)
  list(APPEND HEADERS XSLTUtils.h)
endif()
if(EGL_FOUND)
  list(APPEND SOURCES EGLUtils.cpp)
  list(APPEND HEADERS EGLUtils.h)
endif()

# The large map trips the clang optimizer
if(CMAKE_CXX_COMPILER_ID STREQUAL Clang)
  set_source_files_properties(Mime.cpp PROPERTIES COMPILE_FLAGS -O0)
endif()

if(NOT CORE_SYSTEM_NAME STREQUAL windows AND NOT CORE_SYSTEM_NAME STREQUAL windowsstore)
  list(APPEND SOURCES GLUtils.cpp)
  list(APPEND HEADERS GLUtils.h)
endif()

if(CORE_SYSTEM_NAME STREQUAL android OR AML_FOUND)
  list(APPEND SOURCES AMLUtils.cpp)
  list(APPEND HEADERS AMLUtils.h)
endif()

if(AML_FOUND)
  list(APPEND HEADERS ScreenshotAML.cpp)
  list(APPEND HEADERS ScreenshotAML.h)
endif()

core_add_library(utils)

if(NOT CORE_SYSTEM_NAME STREQUAL windows AND NOT CORE_SYSTEM_NAME STREQUAL windowsstore)
  if(HAVE_SSE2)
    target_compile_options(${CORE_LIBRARY} PRIVATE -msse2)
  endif()
endif()
