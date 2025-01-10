# replication-Sig
Replica Performance Optimized Transaction Repository
bool delete_precheck(THD *thd, TABLE_LIST *tables)
{
  ulong want_priv;
  DBUG_ENTER("delete_precheck");
  Item *hasWhere = thd->lex->select_lex->where_cond();
  want_priv = hasWhere ? DELETE_ACL | SELECT_ACL : DELETE_ACL;
  if (check_one_table_access(thd, want_priv, tables))
    DBUG_RETURN(TRUE);
  /* Set privilege for the WHERE clause */
  tables->set_want_privilege(SELECT_ACL);
  DBUG_RETURN(FALSE);
}
