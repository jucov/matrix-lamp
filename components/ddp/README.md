# DDP compatibility copy

Source: https://github.com/KaufHA/common/tree/5a20b4a283fe50796b71669f4b772ef6cf3c2044/components/ddp

Copied unchanged except the gamma backup in both effect start() methods and
layout assertions in ddp_light_effect_base.h. ESPHome 2026.10.0 has no
get_gamma_table_object(). Its get_gamma_table() returns GammaTable::lut,
the first member of the standard-layout GammaTable. Recover the original
object address for set_gamma_table(), retaining the original flash LUT and
its gamma_x100 metadata. Null remains null. No gamma values are recomputed.

DDP packet handling, brightness scaling, timeout, and restoration on stop
are unchanged. This adapter targets the ESPHome 2026.10.0 GammaTable layout;
recheck it when upgrading ESPHome. Do not substitute set_gamma_correct():
in 2026.10.0 that deprecated setter does nothing.
