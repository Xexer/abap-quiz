# Source Code Examples

## DSAG ABAP Development Days 2024 Quiz

This quiz was played on May 7th, 2024 in Wiesloch for the ABAP Development Days 2024 organized by DSAG and SAP.

```ABAP
CLASS zcl_bs_demo_dsag_quiz DEFINITION
  PUBLIC FINAL
  CREATE PUBLIC.

  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.

  PRIVATE SECTION.
    TYPES: BEGIN OF t_data,
             id   TYPE c LENGTH 5,
             date TYPE d,
             text TYPE string,
           END OF t_data.
    TYPES t_datas TYPE STANDARD TABLE OF t_data WITH EMPTY KEY
                  WITH NON-UNIQUE SORTED KEY bydate COMPONENTS date.

    METHODS find_the_right_field_1
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS concatente_a_string_2
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS reverse_a_string_3
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS change_some_lines_4
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS value_optional_5
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS value_default_11
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS table_with_error_8
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out
      RAISING   cx_sy_itab_line_not_found.

    METHODS substring_of_a_string_6
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS step_forward_7
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS step_backward_10
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS char_datatype_9
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS determine_line_index_19
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS validate_xsdbool_12
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS number_of_lines_20
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS mapping_tables_13
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS value_appending_14
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS string_template_15
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS filter_by_date_16
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.

    METHODS change_with_ref_17
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out
      RAISING   cx_sy_itab_line_not_found.

    METHODS mapping_tables_except_18
      IMPORTING !out TYPE REF TO if_oo_adt_classrun_out.
ENDCLASS.


CLASS zcl_bs_demo_dsag_quiz IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.
    find_the_right_field_1( out ).
    concatente_a_string_2( out ).
    reverse_a_string_3( out ).
    change_some_lines_4( out ).
    value_optional_5( out ).
    substring_of_a_string_6( out ).
    step_forward_7( out ).
    TRY.
        table_with_error_8( out ).
      CATCH cx_sy_itab_line_not_found.
        out->write( 'CX_SY_ITAB_LINE_NOT_FOUND ausgelöst' ).
    ENDTRY.
    char_datatype_9( out ).
    step_backward_10( out ).
    value_default_11( out ).
    validate_xsdbool_12( out ).
    mapping_tables_13( out ).
    value_appending_14( out ).
    string_template_15( out ).
    filter_by_date_16( out ).
    TRY.
        change_with_ref_17( out ).
      CATCH cx_sy_itab_line_not_found.
        out->write( 'CX_SY_ITAB_LINE_NOT_FOUND ausgelöst' ).
    ENDTRY.
    mapping_tables_except_18( out ).
    determine_line_index_19( out ).
    number_of_lines_20( out ).
  ENDMETHOD.


  METHOD find_the_right_field_1.
    DATA(data) = VALUE t_datas( date = '20240507'
                                ( id = '1' text = 'ABAP' )
                                ( id = '2' text = 'Development' )
                                ( id = '3' text = 'Day' )
                                ( id = '4' text = '2024' ) ).

    DATA(result) = data[ id = '2' ]-date.

    out->write( result ).
  ENDMETHOD.


  METHOD concatente_a_string_2.
    DATA(data) = VALUE string_table( ( `Modern` )
                                     ( `ABAP` ) ).

    DATA(result) = concat_lines_of( table = data
                                    sep   = ' ' ).

    out->write( result ).
  ENDMETHOD.


  METHOD reverse_a_string_3.
    DATA(result) = reverse( `tfnukuZ eid ni duolC PABA tiM` ).

    out->write( result ).
  ENDMETHOD.


  METHOD change_some_lines_4.
    DATA(data) = VALUE string_table( ( `Modern` )
                                     ( `ABAP` )
                                     ( `2024` ) ).

    data[ 1 ] = `Learning`.

    DATA(result) = concat_lines_of( table = data
                                    sep   = ` ` ).

    out->write( result ).
  ENDMETHOD.


  METHOD value_optional_5.
    DATA(data) = VALUE t_datas( date = '20240507'
                                ( id = '1' text = 'ABAP' )
                                ( id = '2' text = 'Development' )
                                ( id = '3' text = 'Day' )
                                ( id = '4' text = '2024' ) ).

    DATA(result) = VALUE #( data[ 5 ] OPTIONAL ).

    out->write( result-text ).
  ENDMETHOD.


  METHOD value_default_11.
    DATA(data) = VALUE t_datas( date = '20240507'
                                ( id = '1' text = 'ABAP' )
                                ( id = '2' text = 'Development' )
                                ( id = '3' text = 'Day' )
                                ( id = '4' text = '2024' ) ).

    DATA(result) = VALUE #( data[ 3 ] DEFAULT VALUE #( id   = 5
                                                       text = 'Error' ) ).

    out->write( result-id ).
  ENDMETHOD.


  METHOD table_with_error_8.
    DATA(data) = VALUE t_datas( date = '20240507'
                                ( id = '1' text = 'ABAP' )
                                ( id = '2' text = 'Development' )
                                ( id = '3' text = 'Day' )
                                ( id = '4' text = '2024' ) ).

    DATA(result) = data[ id = '0' ].

    out->write( result-text ).
  ENDMETHOD.


  METHOD substring_of_a_string_6.
    DATA(text) = `ABAP Development in 2024`.

    DATA(part_one) = substring( val = text
                                off = 20
                                len = 4 ).
    DATA(part_two) = text+0(4).

    out->write( part_one && part_two ).
  ENDMETHOD.


  METHOD step_forward_7.
    DATA(data) = VALUE string_table( ( `A` ) ( `B` ) ( `C` ) ( `D` ) ( `E` ) ( `F` ) ).

    DATA(result) = ``.
    LOOP AT data INTO DATA(line) STEP 2.
      result &&= line.
    ENDLOOP.

    out->write( result ).
  ENDMETHOD.


  METHOD step_backward_10.
    DATA(data) = VALUE string_table( ( `A` ) ( `B` ) ( `C` ) ( `D` ) ( `E` ) ( `F` ) ).

    DATA(result) = ``.
    LOOP AT data INTO DATA(line) STEP -3.
      result &&= line.
    ENDLOOP.

    out->write( result ).
  ENDMETHOD.


  METHOD char_datatype_9.
    DATA(identifier) = 3.

    DATA(result) = SWITCH #( identifier
                             WHEN 1 THEN 'ONE'
                             WHEN 2 THEN 'TWO'
                             WHEN 3 THEN 'THREE' ).

    out->write( result ).
  ENDMETHOD.


  METHOD determine_line_index_19.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'E' text = 'Day' )
                                ( id = 'F' text = '2024' ) ).

    DATA(result) = line_index( data[ id = 'D' ] ).

    out->write( result ).
  ENDMETHOD.


  METHOD validate_xsdbool_12.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'E' text = 'Day' )
                                ( id = 'F' text = '2024' ) ).

    DATA(result) = xsdbool( data[ id = 'E' ]-text = 'Development' ).

    out->write( result ).
  ENDMETHOD.


  METHOD number_of_lines_20.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'E' text = 'Day' )
                                ( id = 'F' text = '2024' ) ).

    DATA(result) = lines( data ).

    out->write( result ).
  ENDMETHOD.


  METHOD mapping_tables_13.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'E' text = 'Day' )
                                ( id = 'F' text = '2024' ) ).

    DATA(mapped) = CORRESPONDING t_datas( data MAPPING text = id ).
    DATA(result) = mapped[ 3 ]-text.

    out->write( result ).
  ENDMETHOD.


  METHOD value_appending_14.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'E' text = 'Day' )
                                ( id = 'F' text = '2024' ) ).

    DATA(new_data) = VALUE t_datas( BASE data
                                    ( id = 'G' text = 'Wiesloch' )
                                    ( id = 'H' text = 'SAP' ) ).
    DATA(result) = lines( new_data ).

    out->write( result ).
  ENDMETHOD.


  METHOD string_template_15.
    DATA(magic_number) = CONV char6( 14 ).

    DATA(result) = |MN: { magic_number ALPHA = IN }|.

    out->write( result ).
  ENDMETHOD.


  METHOD filter_by_date_16.
    DATA(data) = VALUE t_datas( ( id = 'A' date = '20240506' )
                                ( id = 'B' date = '20240507' )
                                ( id = 'C' date = '20240508' )
                                ( id = 'D' date = '20240509' ) ).

    DATA(filtered) = FILTER #( data USING KEY bydate WHERE date = CONV d( '20240507' ) ).

    DATA(result) = filtered[ 1 ]-id.

    out->write( result ).
  ENDMETHOD.


  METHOD change_with_ref_17.
    DATA(data) = VALUE t_datas( ( id = 'A' date = '20240506' )
                                ( id = 'B' date = '20240507' )
                                ( id = 'C' date = '20240508' ) ).

    DATA(ref) = REF #( data[ id = 'B' ] ).
    ref->id   = 'Z'.
    ref->date = '20240510'.

    DATA(result) = data[ id = 'B' ]-date.

    out->write( result ).
  ENDMETHOD.


  METHOD mapping_tables_except_18.
    DATA(data) = VALUE t_datas( ( id = 'A' text = 'ABAP' )
                                ( id = 'B' text = 'Development' )
                                ( id = 'C' text = 'Day' )
                                ( id = 'D' text = '2024' ) ).

    DATA(mapped) = CORRESPONDING t_datas( data EXCEPT text ).
    DATA(result) = mapped[ 1 ]-text.

    out->write( result ).
  ENDMETHOD.
ENDCLASS.
```