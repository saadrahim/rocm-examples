# MIT License
#
# Copyright (c) 2022 Advanced Micro Devices, Inc. All rights reserved.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

ROCM_INSTALL_DIR = /opt/rocm
HIPCXX = $(ROCM_INSTALL_DIR)/bin/hipcc
CXX_STD = c++17
COMMON_INCLUDE_DIR = ../../../Common
ROCPRIM_INCLUDE_DIR = $(ROCM_INSTALL_DIR)/include

rocprim_device_sum: main.hip $(COMMON_INCLUDE_DIR)/example_utils.hpp
	$(HIPCXX) $< -std=$(CXX_STD) -isystem $(ROCPRIM_INCLUDE_DIR) -I $(COMMON_INCLUDE_DIR) -o $@ -D__HIP_PLATFORM_AMD__

clean:
	rm -f rocprim_device_sum

.PHONY: clean
