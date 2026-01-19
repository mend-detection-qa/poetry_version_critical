# Test Case: Poetry Version Critical - DEPENDENCY FAILURE TEST

## Package Manager
Poetry

## Python Version Detection
- **Source**: .python-version (PRIORITY #1)
- **Expected Version**: 3.12.0
- **Conflict**: pyproject.toml says ^3.8 (SHOULD BE IGNORED)

## Dependencies (CRITICAL)
- `numpy>=1.26.0` - **REQUIRES Python >=3.9**
- `pandas>=2.1.0` - **REQUIRES Python >=3.9**

## Test Purpose
**CRITICAL DEPENDENCY TEST** - This is NOT just version detection, this tests if dependencies can actually be installed.

### Why This Test Matters
If the tool incorrectly uses `^3.8` from pyproject.toml instead of `3.12.0` from .python-version:
- ❌ **Installation WILL FAIL** with Python 3.8
- ❌ numpy 1.26+ is incompatible with Python 3.8
- ❌ pandas 2.1+ is incompatible with Python 3.8

If the tool correctly uses `3.20.0` from .python-version:
- ✅ **Installation SUCCEEDS** with Python 3.12
- ✅ All dependencies resolve correctly
- ✅ No version conflicts

## Expected Behavior
1. Tool must detect .python-version as HIGHEST priority
2. Tool must use Python 3.10.0 (NOT ^3.8 from pyproject.toml)
3. Dependencies install successfully
4. If tool uses wrong version, test FAILS at dependency installation

## Real-World Impact
This simulates production scenarios where:
- Legacy pyproject.toml specifies older Python
- .python-version specifies current Python
- Modern dependencies require newer Python
- **Wrong version detection = production deployment failure**
