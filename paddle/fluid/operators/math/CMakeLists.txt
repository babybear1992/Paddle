add_subdirectory(detail)

if(WITH_GPU)
    nv_library(math_function SRCS math_function.cc math_function.cu im2col.cc im2col.cu DEPS cblas device_context framework_proto)
    nv_test(math_function_gpu_test SRCS math_function_test.cu DEPS math_function tensor)
    nv_library(selected_rows_functor SRCS selected_rows_functor.cc selected_rows_functor.cu DEPS selected_rows math_function)
    nv_test(selected_rows_functor_gpu_test SRCS selected_rows_functor_test.cu DEPS selected_rows_functor)
    nv_library(softmax SRCS softmax.cc softmax.cu DEPS device_context)
    nv_library(cross_entropy SRCS cross_entropy.cc cross_entropy.cu DEPS device_context)
    nv_library(pooling SRCS pooling.cc pooling.cu DEPS device_context)
    nv_library(depthwise_conv SRCS depthwise_conv.cu DEPS device_context)
    nv_library(sequence_pooling SRCS sequence_pooling.cc sequence_pooling.cu DEPS device_context math_function)
    nv_library(vol2col SRCS vol2col.cc vol2col.cu DEPS device_context tensor)
    nv_library(context_project SRCS context_project.cc context_project.cu DEPS device_context math_function)
    nv_library(sequence2batch SRCS sequence2batch.cc sequence2batch.cu DEPS device_context tensor math_function)
    nv_library(sequence_padding SRCS sequence_padding.cc sequence_padding.cu DEPS lod_tensor device_context)
    nv_library(sequence_scale SRCS sequence_scale.cc sequence_scale.cu DEPS lod_tensor device_context)
    nv_library(lstm_compute SRCS lstm_compute.cc lstm_compute.cu DEPS device_context activation_functions)
    nv_library(maxouting SRCS maxouting.cc maxouting.cu DEPS device_context)
    nv_library(unpooling SRCS unpooling.cc unpooling.cu DEPS device_context)
    nv_library(gru_compute SRCS gru_compute.cc gru_compute.cu DEPS device_context activation_functions math_function)
    nv_library(cos_sim_functor SRCS cos_sim_functor.cc cos_sim_functor.cu DEPS device_context)
    nv_library(concat_functor SRCS concat.cc concat.cu DEPS device_context tensor)
else()
    cc_library(math_function SRCS math_function.cc im2col.cc DEPS cblas device_context framework_proto)
    cc_library(selected_rows_functor SRCS selected_rows_functor.cc DEPS selected_rows math_function)
    cc_library(softmax SRCS softmax.cc DEPS device_context)
    cc_library(cross_entropy SRCS cross_entropy.cc DEPS device_context)
    cc_library(pooling SRCS pooling.cc DEPS device_context)
    cc_library(sequence_pooling SRCS sequence_pooling.cc DEPS device_context math_function)
    cc_library(vol2col SRCS vol2col.cc DEPS device_context tensor)
    cc_library(context_project SRCS context_project.cc DEPS device_context math_function)
    cc_library(sequence2batch SRCS sequence2batch.cc DEPS device_context tensor math_function)
    cc_library(sequence_padding SRCS sequence_padding.cc DEPS lod_tensor device_context)
    cc_library(sequence_scale SRCS sequence_scale.cc DEPS lod_tensor device_context)
    cc_library(lstm_compute SRCS lstm_compute.cc DEPS device_context activation_functions)
    cc_library(maxouting SRCS maxouting.cc DEPS device_context)
    cc_library(unpooling SRCS unpooling.cc DEPS device_context)
    cc_library(gru_compute SRCS gru_compute.cc DEPS device_context activation_functions math_function)
    cc_library(cos_sim_functor SRCS cos_sim_functor.cc DEPS device_context)
    cc_library(concat_functor SRCS concat.cc DEPS device_context tensor)
endif()

cc_test(math_function_test SRCS math_function_test.cc DEPS math_function tensor)
cc_test(selected_rows_functor_test SRCS selected_rows_functor_test.cc DEPS selected_rows_functor)
cc_test(im2col_test SRCS im2col_test.cc DEPS math_function tensor)
cc_test(vol2col_test SRCS vol2col_test.cc DEPS vol2col tensor)
cc_test(sequence_padding_test SRCS sequence_padding_test.cc DEPS sequence_padding)
cc_test(concat_test SRCS concat_test.cc DEPS concat_functor tensor)
