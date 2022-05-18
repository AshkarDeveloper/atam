.global hamming_weight, negate_first_k, bring_balance_to_the_word, read_input

.section .bss
.lcomm path, 1024

.section .text
read_input:
  ret

hamming_weight:
movq (%rdi), %rdx
movq $0, %rbx
len_loop:
leaq (%rdx,%rsi,8), %rdx 
sub %rdx, 8
cmp $0, %rsi
jz end_len_loop
dec %rsi

loop_HW1:
sal (%rdx)
jb label1_HW1
jmp label2_HW1
label1_HW1:
inc %rbx
jmp loop_HW1
label2_HW1:
cmp $0, (%rdx)
je len_loop
jmp loop_HW1

end_len_loop:
movq %rbx, %rax
ret

negate_first_k:
movq %rdi, %rdx
movq %rsi, %rcx
sub $31, %rcx
movq $1, %r8
sal %r8, %rcx
dec %r8
ror %rcx, %r8
movq %rdx, %rax
sub  %rax, %r8
movq %r8, %rax
ret

bring_balance_to_the_word:
movq %rdi, %rbx
movq %rsi, %rcx
movq %rbx, %r12

call hamming_weight
movq $8, %r8
mulq $2, %rax
movq %rcx, %r9
mulq $64, %r9
cmp %r9, %rax
movq $0, %r10
je return_i

movq $1, %r10
flip_loop:
movq %r10, %rax
divq $8
movq $0, %r11
not_loop:
cmp %r11, %rax
je neg_what_left
movq %r11, %r13
mulq $8, %r13
addq %r13, %rbx
not (%rbx)
inc %r11
jmp not_loop

neg_what_left:
movq %r11, %r13
mulq $8, %r13
addq %r13, %rbx

movq (%rbx), %rdi
movq %rdx, %rsi
call negate_first_k
mulq $8, %r11
addq %rbx, %r11
movq %rax, (%rbx)

jmp check
cont:
movq %r12, %rbx
/*negate again*/
movq %r10, %rax
divq $8
movq $0, %r11
not_loop:
cmp %r11, %rax
je neg_what_left
movq %r11, %r13
mulq $8, %r13
addq %r13, %rbx
not (%rbx)
inc %r11
jmp not_loop

neg_what_left:
movq %r11, %r13
mulq $8, %r13
addq %r13, %rbx

movq (%rbx), %rdi
movq %rdx, %rsi
call negate_first_k
mulq $8, %r11
addq %rbx, %r11
movq %rax, (%rbx)
/*end of negate again*/

inc %r10
jmp flip_loop

check:
call hamming_weight
movq $8, %r8
mulq $2, %rax
movq %rcx, %r9
mulq $64, %r9
cmp %r9, %rax
je return_i
jmp cont

return_i:
movq %r10, %rax
ret
