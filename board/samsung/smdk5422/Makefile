#
# Copyright (C) 2013 Samsung Electronics
#
# See file CREDITS for list of people who contributed to this
# project.
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation; either version 2 of
# the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston,
# MA 02111-1307 USA
#

include $(TOPDIR)/config.mk

LIB	= $(obj)lib$(BOARD).o

SOBJS	:= lowlevel_init.o

COBJS	:= clock_init.o
ifdef CONFIG_CPU_EXYNOS5422_EVT0
COBJS	+= dmc.o
COBJS	+= pmu.o
else
COBJS	+= dmc_init.o
endif
COBJS	+= pmic.o
ifdef CONFIG_CPU_EXYNOS5422_EVT0
ifdef CONFIG_MACH_UNIVERSAL5422
COBJS	+= companion_pmic.o
else
COBJS	+= pmic_lm3560.o
endif
endif
COBJS	+= smc.o

ifdef CONFIG_TZPC
COBJS	+= tzpc_init.o
endif

ifndef CONFIG_SPL_BUILD
COBJS	+= smdk5422.o
endif

ifdef CONFIG_SPL_BUILD
COBJS	+= mmc_boot.o
endif

ifdef CONFIG_EXYNOS_THERMAL
COBJS	+= tmu.o
endif

SRCS	:= $(SOBJS:.o=.S) $(COBJS:.o=.c)
OBJS	:= $(addprefix $(obj),$(COBJS) $(SOBJS))

ALL	:=	 $(obj).depend $(LIB)

all:	$(ALL)

$(LIB):	$(OBJS)
	$(call cmd_link_o_target, $(OBJS))

#########################################################################

# defines $(obj).depend target
include $(SRCTREE)/rules.mk

sinclude $(obj).depend

#########################################################################
