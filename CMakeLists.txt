include(platform/platform.cmake)
file(GLOB FCT_PHYS_CORE_SOURCES
        LIST_DIRECTORIES false
        CONFIGURE_DEPENDS
        "./src/core/*.cpp"
)
file(GLOB FCT_PHYS_CORE_HEADERS
        LIST_DIRECTORIES false
        CONFIGURE_DEPENDS
        "./src/core/*.h"
        "./src/core/*.hpp"
)
# bullet
file(GLOB FCT_PHYS_BULLET_CORE_SOURCES
        LIST_DIRECTORIES false
        CONFIGURE_DEPENDS
        "./src/core/BT_*.cpp"
)
file(GLOB FCT_PHYS_BULLET_CORE_HEADERS
        LIST_DIRECTORIES false
        CONFIGURE_DEPENDS
        "./src/core/BT_*.h"
        "./src/core/BT_*.hpp"
)
list(REMOVE_ITEM FCT_PHYS_CORE_SOURCES ${FCT_PHYS_BULLET_CORE_SOURCES})
list(REMOVE_ITEM FCT_PHYS_CORE_HEADERS ${FCT_PHYS_BULLET_CORE_HEADERS})

set(FCT_PHYS_SOURCES
        ${FCT_PHYS_CORE_SOURCES}
        ${FCT_PHYS_BULLET_CORE_SOURCES}
)

set(FCT_PHYS_HEADERS
        ${FCT_PHYS_CORE_HEADERS}
        ${FCT_PHYS_BULLET_CORE_HEADERS}
)

add_library(FCT_Phys STATIC
        ${FCT_PHYS_SOURCES}
        ${FCT_PHYS_HEADERS}
)
find_package(Bullet CONFIG REQUIRED)
target_link_libraries(FCT_Phys PRIVATE ${BULLET_LIBRARIES})
