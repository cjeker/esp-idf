idf_build_get_property(target IDF_TARGET)

set(srcs "src/esp_timer.c"
         "src/ets_timer_legacy.c")

if(CONFIG_ESP_TIMER_IMPL_FRC2)
    list(APPEND srcs "src/esp_timer_impl_frc_legacy.c")
elseif(CONFIG_ESP_TIMER_IMPL_TG0_LAC)
    list(APPEND srcs "src/esp_timer_impl_lac.c")
elseif(CONFIG_ESP_TIMER_IMPL_SYSTIMER)
    list(APPEND srcs "src/esp_timer_impl_systimer.c")
endif()

idf_component_register(SRCS "${srcs}"
                    INCLUDE_DIRS include
                    PRIV_INCLUDE_DIRS private_include
                    REQUIRES esp_common
                    PRIV_REQUIRES soc driver "${target}")
