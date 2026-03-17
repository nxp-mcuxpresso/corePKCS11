#
# Copyright 2024-2026 NXP
#
# SPDX-License-Identifier: MIT
#

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.template)
    # Template/config header is kept in this NXP integration repo.
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
        SOURCES ../corepkcs11-upstream/source/core_pkcs11.c
                ../corepkcs11-upstream/source/core_pki_utils.c
                ../corepkcs11-upstream/source/include/core_pkcs11.h
                ../corepkcs11-upstream/source/include/core_pkcs11_config_defaults.h
                ../corepkcs11-upstream/source/include/core_pkcs11_pal.h
                ../corepkcs11-upstream/source/include/core_pki_utils.h
    )
    mcux_add_include(
        INCLUDES ../corepkcs11-upstream/source/include
    )
endif()

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.mbedtls)
    mcux_add_source(
        SOURCES ../corepkcs11-upstream/source/portable/mbedtls/core_pkcs11_mbedtls.c
    )
endif()

if (CONFIG_MCUX_COMPONENT_middleware.freertos.corepkcs11.mbedtls_utils)
    mcux_add_source(
        SOURCES ../corepkcs11-upstream/source/dependency/3rdparty/mbedtls_utils/mbedtls_utils.c
                ../corepkcs11-upstream/source/dependency/3rdparty/mbedtls_utils/mbedtls_utils.h
    )
    mcux_add_include(
        INCLUDES ../corepkcs11-upstream/source/dependency/3rdparty/mbedtls_utils
    )
    mcux_add_configuration(
        CC "-DMBEDTLS_THREADING_ALT\
            -DMBEDTLS_THREADING_C"
    )
endif()
