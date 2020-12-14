# Assignment3

##The following are the changes made in the files:
##1. cpuid.c
##2. cpuid.h
##3. vmx.c
*******************Changes in cpuid.h***********************
/* Instrumentation functions */
void add_exit(void);
void add_exit_for_reason(u32 exit_reason);
void add_exit_time(u64 time_taken);
void add_exit_time_for_reason(u64 time_taken, u32 exit_reason);
**********************Changes end**************************


*****************Changes made in cpuid.c*********************
int is_exit_reason_valid(u32 exit_reason)
{
  int rtv = 0;

  switch (exit_reason) {
  case EXIT_REASON_EXCEPTION_NMI: rtv = 1; break;
  case EXIT_REASON_EXTERNAL_INTERRUPT: rtv = 1; break;
  case EXIT_REASON_TRIPLE_FAULT: rtv = 1; break;
  case EXIT_REASON_INIT_SIGNAL: rtv = 1; break;
  case EXIT_REASON_INTERRUPT_WINDOW: rtv = 1; break;
  case EXIT_REASON_NMI_WINDOW: rtv = 1; break;
  case EXIT_REASON_TASK_SWITCH: rtv = 1; break;
  case EXIT_REASON_CPUID: rtv = 1; break;
  case EXIT_REASON_HLT: rtv = 1; break;
  case EXIT_REASON_INVD: rtv = 1; break;
  case EXIT_REASON_INVLPG: rtv = 1; break;
  case EXIT_REASON_RDPMC: rtv = 1; break;
  case EXIT_REASON_RDTSC: rtv = 1; break;
  case EXIT_REASON_VMCALL: rtv = 1; break;
  case EXIT_REASON_VMCLEAR: rtv = 1; break;
  case EXIT_REASON_VMLAUNCH: rtv = 1; break;
  case EXIT_REASON_VMPTRLD: rtv = 1; break;
  case EXIT_REASON_VMPTRST: rtv = 1; break;
  case EXIT_REASON_VMREAD: rtv = 1; break;
  case EXIT_REASON_VMRESUME: rtv = 1; break;
  case EXIT_REASON_VMWRITE: rtv = 1; break;
  case EXIT_REASON_VMOFF: rtv = 1; break;
  case EXIT_REASON_VMON: rtv = 1; break;
  case EXIT_REASON_CR_ACCESS: rtv = 1; break;
  case EXIT_REASON_DR_ACCESS: rtv = 1; break;
  case EXIT_REASON_IO_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_MSR_READ: rtv = 1; break;
  case EXIT_REASON_MSR_WRITE: rtv = 1; break;
  case EXIT_REASON_INVALID_STATE: rtv = 1; break;
  case EXIT_REASON_MSR_LOAD_FAIL: rtv = 1; break;
  case EXIT_REASON_MWAIT_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_MONITOR_TRAP_FLAG: rtv = 1; break;
  case EXIT_REASON_MONITOR_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_PAUSE_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_MCE_DURING_VMENTRY: rtv = 1; break;
  case EXIT_REASON_TPR_BELOW_THRESHOLD: rtv = 1; break;
  case EXIT_REASON_APIC_ACCESS: rtv = 1; break;
  case EXIT_REASON_EOI_INDUCED: rtv = 1; break;
  case EXIT_REASON_GDTR_IDTR: rtv = 1; break;
  case EXIT_REASON_LDTR_TR: rtv = 1; break;
  case EXIT_REASON_EPT_VIOLATION: rtv = 1; break;
  case EXIT_REASON_EPT_MISCONFIG: rtv = 1; break;
  case EXIT_REASON_INVEPT: rtv = 1; break;
  case EXIT_REASON_RDTSCP: rtv = 1; break;
  case EXIT_REASON_PREEMPTION_TIMER: rtv = 1; break;
  case EXIT_REASON_INVVPID: rtv = 1; break;
  case EXIT_REASON_WBINVD: rtv = 1; break;
  case EXIT_REASON_XSETBV: rtv = 1; break;
  case EXIT_REASON_APIC_WRITE: rtv = 1; break;
  case EXIT_REASON_RDRAND: rtv = 1; break;
  case EXIT_REASON_INVPCID: rtv = 1; break;
  case EXIT_REASON_VMFUNC: rtv = 1; break;
  case EXIT_REASON_ENCLS: rtv = 1; break;
  case EXIT_REASON_RDSEED: rtv = 1; break;
  case EXIT_REASON_PML_FULL: rtv = 1; break;
  case EXIT_REASON_XSAVES: rtv = 1; break;
  case EXIT_REASON_XRSTORS: rtv = 1; break;
  case EXIT_REASON_UMWAIT: rtv = 1; break;
  case EXIT_REASON_TPAUSE: rtv = 1; break;
  default: rtv = 0; break;
  };

  return rtv;
}


int is_exit_type_enabled_in_kvm(u32 exit_reason)
{
  int rtv = 0;
  
  switch(exit_reason) {
  case EXIT_REASON_EXCEPTION_NMI: rtv = 1; break;
  case EXIT_REASON_EXTERNAL_INTERRUPT: rtv = 1; break;
  case EXIT_REASON_TRIPLE_FAULT: rtv = 1; break;
  case EXIT_REASON_NMI_WINDOW: rtv = 1; break;
  case EXIT_REASON_IO_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_CR_ACCESS: rtv = 1; break;
  case EXIT_REASON_DR_ACCESS: rtv = 1; break;
  case EXIT_REASON_CPUID: rtv = 1; break;
  case EXIT_REASON_MSR_READ: rtv = 1; break;
  case EXIT_REASON_MSR_WRITE: rtv = 1; break;
  case EXIT_REASON_INTERRUPT_WINDOW: rtv = 1; break;
  case EXIT_REASON_HLT: rtv = 1; break;
  case EXIT_REASON_INVD: rtv = 1; break;
  case EXIT_REASON_INVLPG: rtv = 1; break;
  case EXIT_REASON_RDPMC: rtv = 1; break;
  case EXIT_REASON_VMCALL: rtv = 1; break;
  case EXIT_REASON_VMCLEAR: rtv = 1; break;
  case EXIT_REASON_VMLAUNCH: rtv = 1; break;
  case EXIT_REASON_VMPTRLD: rtv = 1; break;
  case EXIT_REASON_VMPTRST: rtv = 1; break;
  case EXIT_REASON_VMREAD: rtv = 1; break;
  case EXIT_REASON_VMRESUME: rtv = 1; break;
  case EXIT_REASON_VMWRITE: rtv = 1; break;
  case EXIT_REASON_VMOFF: rtv = 1; break;
  case EXIT_REASON_VMON: rtv = 1; break;
  case EXIT_REASON_TPR_BELOW_THRESHOLD: rtv = 1; break;
  case EXIT_REASON_APIC_ACCESS: rtv = 1; break;
  case EXIT_REASON_APIC_WRITE: rtv = 1; break;
  case EXIT_REASON_EOI_INDUCED: rtv = 1; break;
  case EXIT_REASON_WBINVD: rtv = 1; break;
  case EXIT_REASON_XSETBV: rtv = 1; break;
  case EXIT_REASON_TASK_SWITCH: rtv = 1; break;
  case EXIT_REASON_MCE_DURING_VMENTRY: rtv = 1; break;
  case EXIT_REASON_GDTR_IDTR: rtv = 1; break;
  case EXIT_REASON_LDTR_TR: rtv = 1; break;
  case EXIT_REASON_EPT_VIOLATION: rtv = 1; break;
  case EXIT_REASON_EPT_MISCONFIG: rtv = 1; break;
  case EXIT_REASON_PAUSE_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_MWAIT_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_MONITOR_TRAP_FLAG: rtv = 1; break;
  case EXIT_REASON_MONITOR_INSTRUCTION: rtv = 1; break;
  case EXIT_REASON_INVEPT: rtv = 1; break;
  case EXIT_REASON_INVVPID: rtv = 1; break;
  case EXIT_REASON_RDRAND: rtv = 1; break;
  case EXIT_REASON_RDSEED: rtv = 1; break;
  case EXIT_REASON_PML_FULL: rtv = 1; break;
  case EXIT_REASON_INVPCID: rtv = 1; break;
  case EXIT_REASON_VMFUNC: rtv = 1; break;
  case EXIT_REASON_PREEMPTION_TIMER: rtv = 1; break;
  case EXIT_REASON_ENCLS: rtv = 1; break;
  default: rtv = 0; break;
  };

  return rtv;
}

int kvm_emulate_cpuid(struct kvm_vcpu *vcpu)
{
	u32 eax, ebx, ecx, edx;
	if (cpuid_fault_enabled(vcpu) && !kvm_require_cpl(vcpu, 0))
		return 1;

	eax = kvm_rax_read(vcpu);
	ecx = kvm_rcx_read(vcpu);
	if (eax  ==  0x4fffffff) {
	    printk("***********DEBUG_BEGIN***********\n");
	    printk("**** EAX: %u\n", eax);
	    ebx = ( (atomic64_read(&exits_time) >> 32) );
	    ecx = ( (atomic64_read(&exits_time) & 0x00000000FFFFFFFF ));
	    eax = atomic_read(&exits);
	    printk("**** (Total number of exits: %u EAX:= %u", atomic_read(&exits), eax);
	    printk("**** EBX:= %u", ebx);
	    printk("**** ECX:= %u", ecx);
	    printk("**** Exit_Reason : ALL , ExitCount : %u\n",eax); //Debug Statement
	    printk("***********DEBUG_END***********\n");
	} else if(eax  ==  0x4ffffffe) {
	  printk("***********DEBUG_BEGIN***********\n");
	  printk("**** EAX: %u\n", eax);
	  printk("**** ECX: %u\n", ecx);
	  printk("**** Input exit reason: %u\n", ecx);
	  // Check if exit number is valid 
	  if (is_exit_reason_valid(ecx)) {
	    // Check if exit type is enabled
	    if (is_exit_type_enabled_in_kvm(ecx)) {
	      // If the exit type is valid and if the exit type is enabled
	      eax = atomic_read(&exits_per_reason[ecx]);
	      printk("**** Exit_Reason : %u , ExitCount : %u\n", ecx, eax);
	    } else {
	      printk("**** Exit type (reason): %u is not supported/enabled in KVM\n", ecx);
	      // If the exit type is valid and if the exit type is disabled
	      eax = 0x0;
	      ebx = 0x0;
	      ecx = 0x0;
	      edx = 0x0;
	    }
	  } else {
	    printk("**** Exit reason: %u is invalid\n", ecx);
	    eax = 0x0;
	    ebx = 0x0;
	    ecx = 0x0;
	    edx = 0xFFFFFFFF;
	  }
	  printk("***********DEBUG_END***********\n");
	} else {
	    kvm_cpuid(vcpu, &eax, &ebx, &ecx, &edx, true);
	}

	kvm_rax_write(vcpu, eax);
	kvm_rbx_write(vcpu, ebx);
	kvm_rcx_write(vcpu, ecx);
	kvm_rdx_write(vcpu, edx);
	return kvm_skip_emulated_instruction(vcpu);
}

/* Functions to update the exit info:
   1) total number of exits
   2) total number of exits per reason
   3) total time for all the exits
   4) total time per exit reason
 */
void add_exit(void) {
  atomic_inc(&exits);
}

void add_exit_for_reason(u32 exit_reason) {
  atomic_inc(&exits_per_reason[exit_reason]);
}

void add_exit_time(u64 time_taken) {
  atomic64_add(time_taken, &exits_time);
}

void add_exit_time_for_reason(u64 time_taken, u32 exit_reason){
  atomic64_add(time_taken, &exit_time_per_reason[exit_reason]);
}
*************************Changes end************************
******************Changes in vmx.c*****************
/*Anupama Kurudi Code Edit*/
/* Wrapper function over vmx_handle_exit */
static int vmx_handle_exit(struct kvm_vcpu *vcpu, fastpath_t exit_fastpath)
{
  static int result = 0;
  u64 start_t, end_t, total_t;

  struct vcpu_vmx *vmx = to_vmx(vcpu);
  u32 exit_reason = vmx->exit_reason;

  // Every time the guest has exited, increment the number of exits
  add_exit();

  // Increment the number of exits corresponding to the 
  // exit_reason
  add_exit_for_reason(exit_reason);

  // Record the begin time of the exit
  start_t = rdtsc();

  // Call the actual exit handler
  result = vmx_handle_exit_int(vcpu, exit_fastpath);
  
  // Record the time at the end of the exit
  end_t = rdtsc();
  total_t = (end_t - start_t);
  
  // Add exit time for all exits
  add_exit_time(total_t);

  // Record the exit time for the current exit reason
  // if the exit_reason is within the max_exit_handlers
  add_exit_time_for_reason(total_t, exit_reason);
  
  return result;
}
**************Changes END****************************
