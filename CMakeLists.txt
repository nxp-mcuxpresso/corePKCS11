#
# Copyright 2024 NXP
#
# SPDX-License-Identifier: MIT
#

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.template)
    mcux_add_source(
        SOURCES template/core_pkcs11_config.h
        CONFIG TRUE
    )
    mcux_add_include(
        TARGET_FILES ['core_pkcs11_config.h'],
        INCLUDES template
    )
endif()

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11)
    mcux_add_source(
        SOURCES source/core_pkcs11.c source/core_pki_utils.c source/include/core_pkcs11.h source/include/core_pkcs11_config_defaults.h source/include/core_pkcs11_pal.h source/include/core_pki_utils.h
    )
    mcux_add_include(
        INCLUDES source/include
    )
endif()

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.mbedtls)
    mcux_add_source(
        SOURCES source/portable/mbedtls/core_pkcs11_mbedtls.c
    )
endif()

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.mbedtls_utils)
    mcux_add_source(
        SOURCES source/dependency/3rdparty/mbedtls_utils/mbedtls_utils.c source/dependency/3rdparty/mbedtls_utils/mbedtls_utils.h
    )
    mcux_add_include(
        INCLUDES source/dependency/3rdparty/mbedtls_utils
    )
    mcux_add_configuration(
        CC "-DMBEDTLS_THREADING_ALT\
            -DMBEDTLS_THREADING_C"
    )
endif()
