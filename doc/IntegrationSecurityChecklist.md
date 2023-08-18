To provide the desired security properties, it is critical to address many details in the integration between the SoC and the Caliptra root-of-trust IP.

#### 1. SoC CPUs running mutable firmware MUST NOT have the ability to directly or indirectly de-assert then re-assert the `cptra_pwrgood` signal without a full reset of every SoC component.

Caliptra is responsible for holding onto early-boot measurements of all firmware loaded into the chip from the outside. If a CPU running vulnerable firmware measured by Caliptra can toggle `cptra_pwrgood` and continue to operate, it could load bogus early-boot measurements into Caliptra, making it attest to something that isn't true (For example, that "new patched firmware" was loaded when "old vulnerable firmware" is actually still running).

This requirement includes power-management or clock-control microcontrollers that can have their firmware loaded from the outside.
